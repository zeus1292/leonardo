# Probe — Product Requirements Document

**Version:** 0.1 (MVP)
**Author:** Akshay Kumar
**Date:** 2026-03-17
**Status:** Draft — Day 1

---

## Problem Statement

AI teams building with LLMs struggle with evaluation in two ways:

1. **They can't test probabilistic outputs the way they test deterministic systems.** Traditional regression testing breaks down when the same prompt produces valid but different outputs. Most teams fall back to vibes-based assessment.

2. **They don't know what to test.** Even teams that want to evaluate properly face a blank-page problem — which metrics matter for their system? What failure modes should they prioritize? Existing tools give you a menu of metrics but no guidance on selection.

**Probe solves both.** It provides a unified framework for deterministic and non-deterministic evaluations, and a thought partner that helps you design the right eval plan for your specific AI system.

---

## Target User (MVP)

**Primary:** Akshay Kumar — solo AI builder, using Probe on personal projects.

**Near-term public:** Solo AI builders, ML engineers, and AI PMs at early-stage companies who:
- Are building RAG pipelines, LLM-powered features, or AI agents
- Have no formal eval framework in place
- Feel the pain of probabilistic outputs and want structured testing
- Are too small for enterprise tools (LangSmith Pro, Arize) but need more than vibes

**Not MVP target:** Large enterprise teams, ML platform teams with dedicated infra, companies with existing eval pipelines.

---

## Goals (MVP)

1. Run deterministic evals across common check types
2. Run non-deterministic evals via LLM-as-judge with configurable rubrics
3. Evaluate RAG pipelines with purpose-built metrics
4. Help users design an eval plan for their system (thought partner)
5. Store eval runs and show pass/fail + score summaries
6. Usable by Akshay on his own AI projects within 5 days

---

## Non-Goals (MVP)

- CI/CD integration (v2)
- Multi-user / team features (v2)
- Real-time production monitoring (v2)
- Custom model fine-tuning for evaluation (v3)
- Visual web UI (v2 — MVP uses CLI + simple report output)

---

## Core Features

### F1 — Eval Suite Management
Define a named collection of eval cases targeting one AI system.

**Fields:**
- Name, description
- System type: `RAG | LLM | AGENT`
- Model/system config (endpoint, model name, parameters)

**Acceptance criteria:**
- Can create, list, and delete suites via CLI
- Suites persist in local SQLite DB
- Each suite has a unique ID

---

### F2 — Eval Case Builder
Define individual test cases within a suite.

**Fields:**
- Input (prompt / query)
- Expected output (optional — required for deterministic, optional for non-det)
- Context (optional — list of strings for RAG evals)
- Eval type: `deterministic | non_deterministic | rag`
- Evaluator: which specific evaluator to use
- Evaluator config: thresholds, rubric text, etc.
- Tags: for filtering and grouping

**Acceptance criteria:**
- Can add cases manually via CLI or import from JSON
- Cases are linked to a suite
- Template cases available for common patterns (RAG Q&A, extraction, chatbot)

---

### F3 — Deterministic Eval Engine
Run binary pass/fail checks against known expected outputs.

**Evaluators (MVP):**
- `exact_match` — case-sensitive equality
- `contains` / `not_contains` — substring presence
- `regex_match` — regex pattern
- `json_schema` — validate output is JSON conforming to schema
- `length_between` — token or character count range
- `starts_with` / `ends_with` — prefix/suffix checks

**Acceptance criteria:**
- Each evaluator returns `{pass: bool, score: 1.0 | 0.0, explanation: str}`
- All deterministic evals run without LLM calls (fast, cheap)
- Results stored per run

---

### F4 — Non-Deterministic Eval Engine (LLM-as-Judge)
Score LLM outputs against rubrics using Claude as the judge.

**Evaluators (MVP):**
- `faithfulness` — is the answer grounded in provided source material?
- `answer_relevance` — does the answer address the question?
- `hallucination` — does the answer contain fabricated information?
- `custom_rubric` — user-defined scoring criteria (1–5 on any dimension)
- `semantic_similarity` — embedding cosine similarity to reference (threshold-based)

**Judge LLM:** Claude (claude-sonnet-4-6 default, configurable)

**Acceptance criteria:**
- Each evaluator returns `{pass: bool, score: float 0-1, explanation: str, confidence: str}`
- Rubric and threshold configurable per case
- Judge prompt is transparent and inspectable
- Results stored per run

---

### F5 — RAG Evaluators
Purpose-built metrics for RAG pipelines requiring question + answer + retrieved contexts.

**Evaluators (MVP):**
- `rag_faithfulness` — claims in answer supported by retrieved context
- `rag_answer_relevance` — answer is relevant to the original question
- `rag_context_precision` — retrieved chunks are relevant to the question
- `rag_context_recall` — all information needed to answer was retrieved

**Acceptance criteria:**
- Takes `{question, answer, contexts[], reference_answer?}` as input
- Returns score 0–1 per metric with explanation
- Can run all 4 as a bundle (`rag_full_suite`)

---

### F6 — Eval Plan Designer (Thought Partner)
The differentiating feature. Describe your AI system → get a recommended eval plan.

**Interaction:**
- User describes their system in plain language (CLI prompt or short form)
- Probe asks 3–5 clarifying questions (system type, use case, failure tolerance, user type)
- Probe generates:
  - Top 5 recommended evaluators with rationale
  - Risk-ranked failure modes for their system type
  - 3 starter eval cases to populate immediately

**Acceptance criteria:**
- Works via CLI interactive session
- Output is a structured eval plan (exportable as JSON + Markdown)
- Starter cases are importable into a suite directly
- Powered by Claude with a well-engineered system prompt

---

### F7 — Test Runner & Results
Execute an eval suite and store/display results.

**CLI:** `probe run --suite <name> [--cases <tag>] [--compare-last]`

**Output (terminal):**
```
Probe Run — my-rag-suite — 2026-03-18 10:32
────────────────────────────────────────────
 Case                      Evaluator            Score   Pass
 Q1: What is...            rag_faithfulness     0.91    ✓
 Q2: How does...           rag_answer_relevance 0.73    ✓
 Q3: When was...           rag_faithfulness     0.44    ✗
 Q4: output format         json_schema          1.00    ✓
────────────────────────────────────────────
 Pass: 3/4 (75%)   Avg score: 0.77   Duration: 4.2s
```

**Acceptance criteria:**
- Results stored in SQLite with run ID, timestamp, all scores
- `--compare-last` shows delta vs previous run (regression detection)
- Export to JSON and Markdown summary

---

## Technical Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Core library | Python | Standard for ML/AI tooling |
| CLI | Typer | Clean, modern Python CLI |
| Data models | Pydantic v2 | Validation + serialization |
| Storage (MVP) | SQLite | Zero-config, local, sufficient for solo use |
| LLM judge | Claude API (claude-sonnet-4-6) | Best reasoning, Akshay already uses it |
| Embeddings | OpenAI text-embedding-3-small | Fast, cheap, good for semantic similarity |
| Packaging | setuptools / PyPI-ready | Importable as `probe-eval` |
| Reporting (MVP) | Rich (terminal) | Beautiful terminal output, no UI needed for v1 |

---

## Data Model

```
EvalSuite
  id: str (uuid)
  name: str
  description: str
  system_type: enum [RAG, LLM, AGENT]
  created_at: datetime

EvalCase
  id: str (uuid)
  suite_id: str (FK)
  input: str
  expected_output: str | None
  contexts: list[str] | None       # for RAG
  eval_type: enum [deterministic, non_deterministic, rag]
  evaluator: str
  evaluator_config: dict            # thresholds, rubric, schema, etc.
  tags: list[str]

EvalRun
  id: str (uuid)
  suite_id: str (FK)
  run_at: datetime
  model_config: dict               # model, temperature, etc.
  summary: dict                    # pass_rate, avg_score, duration

EvalResult
  id: str (uuid)
  run_id: str (FK)
  case_id: str (FK)
  actual_output: str
  score: float                     # 0.0–1.0
  pass: bool
  explanation: str | None
  latency_ms: int
```

---

## MVP Success Criteria

By end of Day 6:
- [ ] `pip install probe-eval` (or local install) works
- [ ] Can define a suite and run deterministic evals in < 5 minutes
- [ ] Can run LLM-as-judge evals on a RAG pipeline
- [ ] Eval plan designer produces useful, specific recommendations
- [ ] Akshay has used it on at least one of his existing projects (Retail Right or InvestorLens)
- [ ] Results are readable and actionable

---

## Open Questions (Day 1)

1. Should the eval plan designer be conversational (back-and-forth) or single-shot (describe → plan)?
2. For semantic similarity — use OpenAI embeddings or a local model (sentence-transformers)?
3. Should MVP include a simple web UI (Streamlit) or stay CLI-only?
4. Linear or GitHub Issues for tracking? (Decided: Linear)
5. Public repo from day 1 (build in public) or private until v1 ships?
