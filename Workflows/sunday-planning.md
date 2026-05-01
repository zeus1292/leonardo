# Workflow: Sunday Planning (/sunday-plan)

Runs every Sunday. Full session: ~60 minutes.
Combines a weekly intelligence scan with sprint planning.

---

## Time Budget

| Step | Time |
|------|------|
| Step 0: Knowledge Scan | ~30–40 min |
| Step 1–2: Orient + Retro | ~5 min |
| Step 3–5: Pick topic + break it down + assign days | ~10–15 min |
| Step 6: Write Sprint | ~5 min |

---

## Step 0: Knowledge Scan (run `/scan` first)

**Before planning anything**, Claude runs the weekly learning scan.

Read `Workflows/learning-scan.md` and execute it fully:
1. Run web searches across Tier 1 and Tier 2 sources
2. Write a new digest entry to `Knowledge/learning-log.md` using `Templates/learning-digest.md`
3. Add any actionable items to `Tasks/backlog.md → ## 🧠 Learning-Driven`

Claude surfaces a quick summary:
> "This week's scan is done. Here's what stood out: [top 2–3 signals]. I've added [N] tasks to the learning backlog."

---

## Step 1: Process the inbox

Read `INBOX.md`. For each entry:
- **Actionable task** → add to `Tasks/backlog.md` under the right track, correctly sized
- **Product idea** → note it for `Projects/product-ideas/` or flag for `/new-idea`
- **Observation or pattern** → hold for the retro in Step 2

After processing, show Akshay what was extracted:
> "Found [N] items in your inbox. Here's what I pulled out: [list]. Clear the inbox now?"

Only clear processed entries after confirmation. Leave anything ambiguous for Akshay to decide.

---

## Step 2: Orient (Claude reads silently)

Read:
- `GOALS.md` — anchor on what matters most this quarter
- `Tasks/backlog.md` — full picture of pending work (including new learning-driven items)
- `Tasks/active-sprint.md` or most recent `Tasks/archive/` entry — what carried over

---

## Step 3: Quick Retro (2 min)

Claude asks:
> "Quick retro on last week — what shipped, what didn't? Any patterns?"

Capture key takeaways. Note carryover items.

---

## Step 4: Capacity Check

Capacity is fixed: **1 hour/day × 7 days = 7 hours/week.**
Target **5 committed hours** (~70%), leaving buffer for interruptions.

Claude asks:
> "Any fixed commitments this week — interviews, calls, travel — that would cut into your hour?"

Adjust accordingly (e.g., a day with an interview → that hour is the interview prep, not a build task).

---

## Step 5: Pick the week's learning topic

Claude asks:
> "What's the one topic you want to go deep on this week?"

Once confirmed, Claude breaks it into 5 daily tasks (Mon–Fri), each scoped to 1 hour:
- Mon–Wed: progressive understanding (concepts → examples → patterns)
- Thu: apply or audit (test it against your own work or OS)
- Fri: synthesize (write a principles doc, implement a change, or ship a take)

Each task gets a concrete "done when..." output — not just time spent.

---

## Step 6: Assign Days

One task per day, Mon–Fri. The topic breakdown from Step 4 is the sprint.

Rules:
- Tasks should build on each other day-over-day — each day's output feeds the next
- Thu and Fri should produce something tangible (a doc, a change, a published take)
- If a day is blocked by commitments, that task slides to the next available day

---

## Step 7: Write the Sprint

Claude writes to `Tasks/active-sprint.md` using `Templates/sprint.md`:
- Week dates, capacity, sprint theme
- Kanban board: Todo items assigned by day
- Time budget table

Claude archives the previous sprint to `Tasks/archive/YYYY-MM-DD.md`.

---

## Step 8: Commit & Close

Claude summarizes:
> "Sprint is set. This week: [theme]. Top priority: [X]. 5 tasks, 5 hours, one per day. See you tomorrow for standup."

---

## Anti-patterns to avoid

- Don't skip the scan — it's what keeps the backlog alive and relevant.
- Don't over-commit. 5 tasks × 1 hour beats 10 tasks × 30 minutes.
- Don't plan tasks that aren't actionable — if it needs definition, the task is "define X" not "do X."
- Don't let scan results crowd out execution. New insights → backlog, not this sprint.
