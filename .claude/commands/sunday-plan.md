You are running the weekly Sunday planning session for Akshay's Personal OS. Full session takes ~60 minutes. Follow these steps exactly.

## Step 1: Load context (silently)
Read:
- `GOALS.md` — current quarter priorities
- `Tasks/backlog.md` — all pending work
- `Tasks/active-sprint.md` — last sprint's state
- Most recent file in `Tasks/archive/` if it exists

## Step 2: Run the learning scan
Tell Akshay: "Starting the weekly scan before we plan — this is what feeds the backlog."

Follow `Workflows/learning-scan.md` exactly:
1. Run web searches across Tier 1 and Tier 2 sources
2. Write a new digest entry to `Knowledge/learning-log.md` using `Templates/learning-digest.md`
3. Add actionable items to `Tasks/backlog.md` under `## 🧠 Learning-Driven`

Surface a brief summary: "Scan done. Here's what stood out: [top 2–3 signals]. Added [N] tasks to learning backlog."

## Step 3: Quick retro
Show a summary of last sprint: Done vs still in Todo/In Progress.
Ask: "What actually shipped, what didn't, any patterns worth noting?"
Wait for response.

## Step 4: Capacity check
Capacity is fixed at 1 hr/day. Ask only:
"Any days this week where you won't have your hour? Interviews, calls, travel?"
Adjust committed tasks accordingly.

## Step 5: Propose the sprint
Pick 5 tasks from `Tasks/backlog.md` that:
- Best align with `GOALS.md` — AI-Native PM Knowledge track is primary
- Are ~1 hour each (M size)
- Include at least 1 learning-driven item from the Sunday scan
- Are actionable as-is

Present as a proposed list. Ask: "Want to swap, cut, or add anything?"
Wait for confirmation.

## Step 6: Assign days
Map confirmed tasks to Mon–Fri, one per day.
Show the day-by-day plan. Ask: "Does this feel right?"

## Step 7: Write the sprint
After confirmation:
1. Archive previous sprint: copy `Tasks/active-sprint.md` to `Tasks/archive/YYYY-MM-DD.md` (Monday date of week just ended)
2. Write new sprint to `Tasks/active-sprint.md` using `Templates/sprint.md`
3. Fill in: week dates, capacity, sprint theme, Kanban Todo with day assignments, time budget

## Step 8: Close
Summarize in 3 lines:
- Sprint theme
- Top priority this week
- Tasks committed by track

Say: "Sprint is set. See you tomorrow for standup."
