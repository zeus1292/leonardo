# Project Brief: Probe

**Track:** AI Product Builder (Passive Income + Proof of Build)
**Started:** 2026-03-17
**Target:** Working MVP by 2026-03-22 (end of sprint)
**Status:** Active — Day 1 (Requirements)

---

## What & Why

**What it is:** An AI evaluation tool that acts as both a *runner* (executes deterministic and non-deterministic evals) and a *thought partner* (helps you design what to evaluate and how).

**Why I'm building it:** Every AI team building with LLMs struggles with evaluation — especially non-deterministic outputs where there's no single correct answer. Existing tools (LangSmith, Braintrust, DeepEval) are runners. None help you design the eval plan. That's the gap Probe fills.

**Why me:** I've lived this pain — at S&P Global with RAG pipelines, at C3 AI with agent evaluation. I've built LLM-Ops frameworks. I understand both the technical and product dimensions of this problem.

**Dual purpose:** Probe is also my Proof of Build — I'm building it with Claude agents, documenting the process publicly, and using it to demonstrate AI product thinking to recruiters and the community.

**Definition of done (MVP):**
- Run deterministic evals (exact match, regex, JSON schema, contains, length)
- Run non-deterministic evals (LLM-as-judge with configurable rubric)
- RAG-specific evaluators (faithfulness, answer relevance, context precision, recall)
- Eval plan designer — describe your AI system → get a recommended eval plan
- Basic results reporting (pass/fail, scores, comparison across runs)
- Usable by Akshay on his own projects

---

## Milestones

1. **Day 1 (Mar 17)** — Requirements, competitive research, PRD, architecture, Linear setup
2. **Day 2 (Mar 18)** — Repo setup, data models, eval case schema, CLI scaffold
3. **Day 3 (Mar 19)** — Deterministic eval engine + test runner
4. **Day 4 (Mar 20)** — Non-deterministic engine (LLM-as-judge, semantic similarity)
5. **Day 5 (Mar 21)** — RAG evaluators + eval plan designer (thought partner)
6. **Day 6 (Mar 22)** — Reporting layer, polish, README, PyPI prep

**Current milestone:** Day 1 — Requirements

---

## Resources

- **Repo:** TBD — create on Day 2
- **Linear project:** probe — set up on Day 1
- **PRD:** `Projects/active/probe/prd.md`
- **Architecture:** `Projects/active/probe/architecture.md`
- **Research:** `Projects/active/probe/research.md`
