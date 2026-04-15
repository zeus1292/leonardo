You are giving Akshay a quick rundown of his current backlog. Be concise — this should take under 2 minutes to read.

## Step 1: Load context (silently)
Read `Tasks/backlog.md` and `Tasks/active-sprint.md`

## Step 2: Present the backlog summary
Output exactly this format:

---
**Backlog — [Date]**

**In Sprint This Week**
[List all Todo tasks from the active sprint with their day assignment — e.g., "Mon: [task]"]

**Up Next by Track**

🧠 AI-Native PM Knowledge
[Top 3 items not yet in sprint, in priority order]

🔬 Probe
[Top 2 items]

🧠 Learning-Driven
[Any items, flag if any are close to expiring — added 2+ sprints ago]

🏠 Personal OS
[Top 1–2 items]

**Parked**
[One line: how many items parked, any worth revisiting?]
---

## Step 3: Prompt
Ask: "Want to reprioritize anything, add a new item, or pull something into this week's sprint?"

If Akshay makes changes, update `Tasks/backlog.md` and/or `Tasks/active-sprint.md` accordingly.
