# Probe — Technical Architecture

**Version:** 0.1 (MVP)
**Date:** 2026-03-17

---

## Repo Structure

```
probe/
├── probe/                        # Core Python package
│   ├── __init__.py
│   ├── cli.py                    # Typer CLI entry point
│   ├── models.py                 # Pydantic data models
│   ├── db.py                     # SQLite storage layer
│   ├── runner.py                 # Eval suite runner (orchestrator)
│   ├── evaluators/
│   │   ├── __init__.py
│   │   ├── deterministic.py      # F3: exact_match, contains, regex, etc.
│   │   ├── llm_judge.py          # F4: LLM-as-judge evaluators
│   │   └── rag.py                # F5: RAG-specific evaluators
│   ├── planner/
│   │   ├── __init__.py
│   │   └── designer.py           # F6: Eval plan designer (thought partner)
│   └── report.py                 # F7: Terminal reporting via Rich
├── tests/
│   ├── test_deterministic.py
│   ├── test_llm_judge.py
│   └── test_rag.py
├── examples/
│   ├── basic_rag_suite.py        # Example: RAG eval in 20 lines
│   └── custom_rubric.py          # Example: custom LLM-as-judge
├── pyproject.toml
├── README.md
└── .env.example
```

---

## Component Architecture

```
┌─────────────────────────────────────────────────────┐
│                    CLI (Typer)                       │
│  probe run / probe suite / probe plan / probe report │
└───────────────────┬─────────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────────┐
│                  Runner                              │
│  Loads suite → executes cases → stores results       │
└──────┬────────────────────┬────────────────┬────────┘
       │                    │                │
┌──────▼──────┐   ┌─────────▼───────┐  ┌────▼──────┐
│Deterministic│   │  LLM-as-Judge   │  │    RAG    │
│  Engine     │   │     Engine      │  │  Engine   │
│             │   │  (Claude API)   │  │(Claude API│
│exact_match  │   │  faithfulness   │  │+ embeds)  │
│contains     │   │  relevance      │  │           │
│regex        │   │  hallucination  │  │rag_faith  │
│json_schema  │   │  custom_rubric  │  │rag_recall │
│length       │   │  semantic_sim   │  │rag_prec   │
└──────┬──────┘   └─────────┬───────┘  └────┬──────┘
       │                    │               │
┌──────▼────────────────────▼───────────────▼────────┐
│                  Storage (SQLite)                    │
│      EvalSuite / EvalCase / EvalRun / EvalResult     │
└─────────────────────────────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────────┐
│              Report (Rich terminal)                  │
│     Pass/fail table, scores, run comparison          │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│           Eval Plan Designer (Separate)              │
│  Input: system description                           │
│  Claude: classify → identify risks → map evaluators  │
│  Output: eval plan + starter cases                   │
└─────────────────────────────────────────────────────┘
```

---

## Key Design Decisions

### 1. Python library first, CLI as the interface
Start as a Python package that can also be used programmatically. This gives:
- Easy integration into existing projects (`from probe import EvalSuite`)
- CLI for interactive use (`probe run --suite my-rag`)
- Path to a web UI later without rewriting core logic

### 2. SQLite for MVP storage
Zero configuration, runs locally, sufficient for solo use with hundreds of eval cases.
Schema is clean enough to migrate to Postgres when multi-user is needed.

### 3. Claude as the judge LLM
Rationale: Akshay already uses Claude, best reasoning capabilities, transparent chain-of-thought for explanations. Judge model is configurable — can swap to GPT-4o or Gemini.

### 4. Evaluator interface (consistent contract)
Every evaluator, regardless of type, returns the same structure:
```python
@dataclass
class EvalScore:
    pass_: bool
    score: float          # 0.0–1.0
    explanation: str
    raw_output: str | None = None
    latency_ms: int = 0
```
This makes the runner generic — it doesn't care what type of evaluator it calls.

### 5. Eval plan designer as a separate module
The thought partner is independent of the eval runner. It produces a plan (JSON + Markdown) that can feed into suite creation, but doesn't require running anything. This keeps concerns separated and makes it testable.

---

## LLM Judge Prompt Design

The faithfulness evaluator prompt (example):

```
System: You are an expert AI evaluation assistant. Your job is to assess
whether an AI-generated answer is faithful to the provided source context.
Faithful means: all claims in the answer are supported by the context.
No external knowledge. No fabrication.

User:
Question: {question}
Context: {context}
Answer: {answer}

Evaluate faithfulness on a scale of 0.0 to 1.0.
- 1.0: Every claim is directly supported by the context
- 0.5: Most claims supported, some extrapolation
- 0.0: Answer contains claims not in the context / fabricated

Respond in JSON:
{
  "score": <float 0-1>,
  "pass": <bool, true if score >= threshold>,
  "explanation": "<one paragraph citing specific supported/unsupported claims>",
  "unsupported_claims": ["<claim 1>", ...]
}
```

---

## CLI Design

```bash
# Suite management
probe suite create --name "my-rag-evals" --type RAG
probe suite list
probe suite show <name>

# Case management
probe case add --suite <name>            # interactive
probe case import --suite <name> --file cases.json

# Running evals
probe run --suite <name>
probe run --suite <name> --tags regression
probe run --suite <name> --compare-last

# Eval plan designer
probe plan --describe                    # interactive session
probe plan --system "RAG pipeline for..." # single-shot

# Reports
probe report --run <run-id>
probe report --suite <name> --last 5    # compare last 5 runs
```

---

## Day-by-Day Build Plan

| Day | Focus | Key deliverables |
|-----|-------|-----------------|
| 2 | Foundation | Repo, pyproject.toml, Pydantic models, SQLite schema, CLI scaffold |
| 3 | Deterministic engine | All 7 deterministic evaluators + runner + Rich report |
| 4 | LLM-as-judge engine | faithfulness, relevance, hallucination, custom_rubric, semantic_sim |
| 5 | RAG + Thought partner | 4 RAG evaluators + eval plan designer + starter case generation |
| 6 | Polish + ship | Run comparison, export, README, examples, PyPI prep |
