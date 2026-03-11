# Workflow: Daily Standup (/standup)

A 5-minute morning check-in. Keep it tight and actionable.

---

## What Claude Does

1. Read `Tasks/active-sprint.md`
2. Identify: what's In Progress, what's next in Todo, what's blocked
3. Present a concise summary

---

## Output Format

> **Standup — [Day, Date]**
>
> **In Progress:**
> - [task]
>
> **Up Next:**
> - [task 1]
> - [task 2]
>
> **Blocked:**
> - [anything blocked, or "nothing blocked"]
>
> **Today's Focus:** [one high-leverage thing based on sprint priorities]
>
> Anything you want to move, update, or flag before you start?

---

## After the Standup

If Akshay updates task status (started, done, blocked), Claude updates `Tasks/active-sprint.md` accordingly.

If it's Friday or the last day of the sprint, Claude prompts:
> "Sprint ends this week — want to do a quick weekly review now, or Sunday?"
