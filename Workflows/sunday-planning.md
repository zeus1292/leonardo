# Workflow: Sunday Planning (/sunday-plan)

Triggered every Sunday. This is the weekly sprint kickoff.
Claude runs this as a structured session with Akshay.

---

## Step 1: Orient (Claude reads silently)

Before saying anything, Claude should read:
- `GOALS.md` — anchor on what matters most this quarter
- `Tasks/backlog.md` — full picture of pending work
- `Tasks/active-sprint.md` (last week's) or most recent `Tasks/archive/` entry — what carried over, what got done

---

## Step 2: Quick Retro (2 min)

Claude asks:
> "Before we plan, quick retro on last week. What shipped? What didn't? Any patterns worth noting?"

Capture key takeaways. Note carryover items.

---

## Step 3: Capacity Check

Claude asks:
> "What's your capacity this week? Any fixed commitments (interviews, calls, travel, appointments)?"

Akshay responds with rough availability. Claude calculates realistic working hours.

---

## Step 4: Prioritization

Claude surfaces the top 8-12 items from the backlog that:
1. Align most directly with current quarter goals
2. Are appropriately sized for available capacity
3. Balance both tracks (job search + product building)

For each, Claude shows: task name, track, estimate, and why it's relevant now.

Claude asks:
> "Here's what I'd pull in this week based on your goals and capacity. Does this feel right, or do you want to swap anything?"

---

## Step 5: Time Boxing

Claude creates a day-by-day time allocation:
- Assigns tasks to specific days (not hours)
- Groups related tasks together
- Protects at least one block for deep work each day
- Leaves buffer for unexpected job search activity (recruiter calls, etc.)

---

## Step 6: Write the Sprint

Claude writes the completed sprint to `Tasks/active-sprint.md`:
- Fills in week dates, capacity, sprint theme
- Populates the Kanban board with Todo items
- Sets the top priority and time budget

Claude also archives the previous sprint to `Tasks/archive/YYYY-MM-DD.md`.

---

## Step 7: Commit & Close

Claude summarizes:
> "This week's sprint is set. Your top priority is [X]. You've got [Y] hours across [Z] days. See you tomorrow for standup."

---

## Anti-patterns to avoid

- Don't over-commit. A 70% full sprint is better than a 110% sprint.
- Don't let job search crowd out building time (or vice versa).
- Don't plan tasks that aren't actionable — if something needs more definition, the task is "define X" not "do X."
