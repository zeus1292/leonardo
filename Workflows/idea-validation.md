# Workflow: Idea Validation (/new-idea [name])

Use this whenever a new product idea surfaces. The goal is to kill bad ideas fast and invest in good ones.

---

## Step 1: Capture (don't filter yet)

Claude opens `Templates/idea-canvas.md`, fills in the name, and asks:
> "Tell me about the idea — what problem does it solve and for who?"

Akshay brain-dumps. Claude captures it verbatim.

---

## Step 2: The Gut Check (60 seconds)

Claude asks 3 quick questions:
1. "Have you personally felt this pain?"
2. "Do you know at least 3 people who would pay for this today?"
3. "Is there a clear reason AI makes this meaningfully better than existing solutions?"

If all 3 are "no" — flag it and file in `Projects/product-ideas/` as low priority.

---

## Step 3: Market Scan

Claude checks `Knowledge/ai-landscape.md` for existing solutions.

Claude also surfaces: Who's already doing this? What's the incumbent solution? Is there a wedge?

---

## Step 4: Monetization Path

Claude checks `Knowledge/passive-income.md` and asks:
> "How does this make money? Walk me through the simplest path from 0 to first dollar."

Must have a clear answer before moving forward. Models to consider:
- SaaS subscription (recurring, scalable)
- Usage-based / API (good for AI tools)
- One-time purchase / template
- Community / membership
- Consulting wrapper (not truly passive, but can be)

---

## Step 5: Build Complexity Check

Given Akshay is a solo builder:
- Can a working prototype be built in 1-2 weeks?
- What's the core technical risk?
- What can be deferred to v2?

---

## Step 6: Score & Decide

Score the idea across 4 dimensions (1-5 each):

| Dimension | Score | Notes |
|-----------|-------|-------|
| Pain strength (how bad is the problem?) | | |
| Willingness to pay (would they pay now?) | | |
| Build complexity (inversely scored) | | |
| Distribution (do you have a path to users?) | | |
| **Total** | /20 | |

- 16-20: Strong signal. Move to active project.
- 10-15: Interesting. Do 3 user conversations before deciding.
- <10: Park it. Revisit later.

---

## Step 7: File It

Save the completed canvas to `Projects/product-ideas/[idea-name].md`.
If moving forward, create a project folder in `Projects/active/[idea-name]/`.
Add relevant tasks to `Tasks/backlog.md`.
