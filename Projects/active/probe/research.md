# Probe — Competitive Research & Eval Taxonomy

*Day 1 research. Use this to sharpen positioning before writing the PRD.*

---

## Competitive Landscape

### LangSmith (LangChain)
- **What it does:** Tracing + observability first. Eval is a secondary module.
- **Strengths:** Deep LangChain integration, widely adopted, good human annotation UX
- **Eval approach:** LLM-as-judge + human feedback. You define the criteria manually.
- **Gap:** Eval design is entirely on you. No guidance on what to test. Tied to LangChain ecosystem.
- **Pricing:** Free tier, paid from $39/mo

### Braintrust
- **What it does:** Purpose-built eval platform with experiments, datasets, scoring functions
- **Strengths:** Clean UI, strong CI/CD integration, good for prompt regression
- **Eval approach:** Custom scoring functions (Python) + LLM-as-judge
- **Gap:** Still just a runner. Requires you to already know what to test and how to score it. No thought partner.
- **Pricing:** Free tier, usage-based paid

### DeepEval
- **What it does:** Open-source Python eval framework with 14+ built-in metrics
- **Strengths:** Rich metric library, pytest integration, Confident AI cloud dashboard
- **Eval approach:** LLM-as-judge for most metrics (faithfulness, hallucination, answer relevance, etc.)
- **Gap:** Metric selection is a menu — no guidance on which metrics matter for your system. Setup overhead is high. Feels like a testing framework, not a product.
- **Pricing:** Open source + paid cloud

### Ragas
- **What it does:** RAG-specific evaluation framework
- **Strengths:** Best-in-class RAG metrics (faithfulness, context precision, context recall, answer relevance)
- **Eval approach:** LLM-as-judge + reference-based
- **Gap:** Only RAG. No general LLM evals. No thought partner. Python library only.
- **Pricing:** Open source

### PromptFoo
- **What it does:** CLI-based prompt eval tool, YAML config
- **Strengths:** Fast, CI-friendly, good for prompt regression testing
- **Eval approach:** Deterministic assertions + LLM-as-judge
- **Gap:** Developer-only. No UI. No non-deterministic guidance. Not designed for RAG.
- **Pricing:** Open source + paid cloud

### Arize / Phoenix
- **What it does:** ML monitoring and observability, eval capabilities added
- **Strengths:** Enterprise-grade, strong tracing, good for production monitoring
- **Gap:** Complex setup, enterprise-focused, overkill for solo builders
- **Pricing:** Enterprise

---

## The Gap Probe Fills

| Capability | LangSmith | Braintrust | DeepEval | Ragas | PromptFoo | **Probe** |
|------------|-----------|------------|----------|-------|-----------|-----------|
| Deterministic evals | ✓ | ✓ | ✓ | ✗ | ✓ | ✓ |
| Non-deterministic evals | ✓ | ✓ | ✓ | ✓ | Partial | ✓ |
| RAG-specific evaluators | Partial | Partial | ✓ | ✓ | ✗ | ✓ |
| Eval plan designer (thought partner) | ✗ | ✗ | ✗ | ✗ | ✗ | **✓** |
| Designed for solo builders | ✗ | Partial | ✓ | ✓ | ✓ | ✓ |
| Clean web UI | ✓ | ✓ | ✓ | ✗ | ✗ | ✓ (v2) |

**Probe's differentiated position:** The only eval tool that helps you design what to evaluate, not just run evaluations. Opinionated, solo-builder-first, starts personal then opens to the public.

---

## Eval Taxonomy

### Deterministic Evaluators
These have known expected outputs. Pass/fail is binary and reproducible.

| Evaluator | Description | Use case |
|-----------|-------------|----------|
| `exact_match` | Output == expected string | Classification, single-answer tasks |
| `contains` | Output contains substring | Keyword presence checks |
| `not_contains` | Output does NOT contain substring | Guardrails, content filtering |
| `regex_match` | Output matches regex pattern | Structured output validation |
| `json_schema` | Output is valid JSON matching schema | Structured extraction |
| `length_between` | Token/char count within range | Output length constraints |
| `latency_under` | Response time < threshold ms | Performance SLAs |
| `starts_with` / `ends_with` | Prefix/suffix checks | Format validation |

### Non-Deterministic Evaluators (LLM-as-Judge)
These use an LLM to score outputs. Results are probabilistic — run multiple times for confidence.

| Evaluator | Description | Score |
|-----------|-------------|-------|
| `faithfulness` | Is the answer grounded in source material? | 0–1 |
| `answer_relevance` | Does the answer address the question? | 0–1 |
| `hallucination` | Does the answer contain fabricated facts? | 0–1 (inverse) |
| `tone_adherence` | Does tone match specified style/persona? | 0–1 |
| `custom_rubric` | Score against a user-defined rubric (1–5 on any dimension) | 0–1 normalized |
| `semantic_similarity` | Embedding cosine similarity to reference | 0–1 |
| `completeness` | Does the answer cover all required aspects? | 0–1 |
| `safety` | Does the output contain harmful content? | 0–1 (inverse) |

### RAG-Specific Evaluators
Require: question, answer, retrieved context(s), optional reference answer.

| Evaluator | Description | Formula |
|-----------|-------------|---------|
| `rag_faithfulness` | Claims in answer supported by context | supported claims / total claims |
| `rag_answer_relevance` | Answer relevant to the original question | LLM judge |
| `rag_context_precision` | Retrieved context is relevant to question | relevant chunks / total chunks |
| `rag_context_recall` | All needed info was retrieved | LLM judge vs reference |
| `rag_groundedness` | Answer stays within context, no hallucination | LLM judge |

---

## Thought Partner Feature — Design Notes

The eval plan designer is Probe's moat. Here's how it should work:

**Input:** User describes their AI system in plain language
> "I have a RAG pipeline that answers questions about financial documents. It retrieves 5 chunks from a Pinecone index and passes them to GPT-4o. Users are financial analysts."

**Probe's process:**
1. Classify the system type (RAG / chatbot / extraction agent / etc.)
2. Identify the highest-risk failure modes for that system type
3. Map failure modes to specific evaluators
4. Recommend an eval plan with rationale
5. Generate 3–5 starter eval cases to populate immediately

**Output:**
> "For a financial RAG system, your top 5 evaluation priorities are:
> 1. Faithfulness — financial claims must be grounded in source docs (high stakes)
> 2. Hallucination — fabricated numbers/dates are critical failures
> 3. Context precision — retrieving irrelevant docs degrades accuracy
> 4. Answer completeness — analysts need full context, not partial answers
> 5. Latency — target < 3s for interactive use
>
> Here are 3 starter test cases based on common failure patterns..."

This turns Probe from a tool into a thinking partner — exactly what teams lack.
