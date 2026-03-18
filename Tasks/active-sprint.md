# Active Sprint

**Week of:** March 15–22, 2026
**Capacity:** 3 hrs/day × 7 days = ~21 hrs | Target 70% committed = ~15 hrs
**Sprint Theme:** Probe — requirements to working MVP

---

## Kanban Board

### 📋 Todo

**Day 1 — Requirements (today)**
- [ ] Review and finalize PRD — answer open questions [#probe] [S]
- [ ] Review architecture doc — confirm stack decisions [#probe] [S]
- [ ] Set up Linear project "Probe" — create all Day 2–6 issues [#probe] [S]
- [ ] Create GitHub repo (public or private — decide today) [#probe] [S]
- [ ] Post on LinkedIn: describe the eval pain point, tease Probe [#probe] [S]

**Day 2 — Foundation**
- [ ] Initialize Python repo with pyproject.toml, package structure [#probe] [M]
- [ ] Write Pydantic models: EvalSuite, EvalCase, EvalRun, EvalResult [#probe] [M]
- [ ] Set up SQLite schema + db.py CRUD layer [#probe] [M]
- [ ] Scaffold CLI with Typer: suite create/list, case add, run commands [#probe] [M]

**Day 3 — Deterministic Engine**
- [ ] Implement exact_match, contains, not_contains evaluators [#probe] [M]
- [ ] Implement regex_match, json_schema evaluators [#probe] [M]
- [ ] Implement length_between, starts_with, ends_with evaluators [#probe] [S]
- [ ] Wire evaluators into runner + store results [#probe] [M]
- [ ] Build Rich terminal report for run output [#probe] [M]

**Day 4 — LLM-as-Judge Engine**
- [ ] Design and test judge prompt for faithfulness [#probe] [M]
- [ ] Implement answer_relevance, hallucination evaluators [#probe] [M]
- [ ] Implement custom_rubric evaluator (user-defined criteria) [#probe] [M]
- [ ] Implement semantic_similarity (embedding cosine) [#probe] [M]
- [ ] Add --compare-last flag to runner for regression detection [#probe] [S]

**Day 5 — RAG Evaluators + Eval Plan Designer**
- [ ] Implement rag_faithfulness, rag_answer_relevance evaluators [#probe] [M]
- [ ] Implement rag_context_precision, rag_context_recall evaluators [#probe] [M]
- [ ] Build eval plan designer: interactive CLI session [#probe] [L]
- [ ] Engineer thought partner prompt: classify → risks → evaluator map → starter cases [#probe] [L]
- [ ] Test designer against Retail Right or InvestorLens as example system [#probe] [M]

**Day 6 — Polish + Ship**
- [ ] Run comparison report (delta vs last run) [#probe] [M]
- [ ] JSON + Markdown export for results [#probe] [S]
- [ ] Write README with quickstart and examples [#probe] [M]
- [ ] Write 2 example scripts (basic RAG suite, custom rubric) [#probe] [S]
- [ ] PyPI packaging prep (pyproject.toml, versioning, test install) [#probe] [M]

**Job Search (parallel)**
- [ ] Update LinkedIn headline + About section [#job] [S]
- [ ] Audit + refresh resume for AI PM positioning [#job] [M]

### 🔄 In Progress

### ✅ Done
- [x] Competitive research — LangSmith, Braintrust, DeepEval, Ragas, PromptFoo [#probe]
- [x] Eval taxonomy — deterministic, non-deterministic, RAG [#probe]
- [x] PRD v0.1 written [#probe]
- [x] Architecture doc written [#probe]

### 🚫 Blocked

---

## This Week's Focus

**Top priority:** Ship a working Probe MVP by end of Day 6
**Secondary:** LinkedIn + resume updated for job search
**Stretch goal:** Run Probe against InvestorLens or Retail Right as a real test case

---

## Time Budget

| Track | Allocated |
|-------|-----------|
| Probe (build) | ~12 hrs |
| Job Search | ~2 hrs |
| Admin / OS | ~1 hr |
| **Total** | ~15 hrs |

---

## Notes

- 2 interviews this week — keep interview days lighter on deep build work
- Linear is the source of truth for Probe tasks — this board mirrors it
- Decision pending: public repo from day 1 (build in public) or private until v1?

---

*Sprint started:* March 15, 2026
*Sprint ends:* March 22, 2026
