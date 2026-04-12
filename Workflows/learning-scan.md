# Workflow: Weekly Learning Scan (/scan)

Runs every Sunday as Step 0 of `/sunday-plan`.
Claude performs a structured intelligence sweep across AI, productivity, and fintech channels.
Output is written to `Knowledge/learning-log.md` and used to update `Tasks/backlog.md`.

---

## Purpose

Surface what's changing in AI, PM, and fintech — then translate signal into action.
Not passive reading. Every insight should map to one of three outcomes:
- A backlog task (learn, build, apply, or research something)
- An update to `Knowledge/ai-landscape.md` or `Knowledge/passive-income.md`
- A product idea worth logging in `Projects/product-ideas/`

---

## Sources to Scan (by priority)

### Tier 1 — Highest signal

| Source | What to look for |
|--------|-----------------|
| r/ProductManagement | Threads on AI in PM workflows, tool pain points, hiring signals |
| r/MachineLearning | Applied AI breakthroughs, new open-source releases |
| r/artificial + r/ChatGPT | Consumer AI behavior shifts, viral tools, emerging use cases |
| Hacker News (Show HN + top) | New AI tools, indie builder launches, PM/founder takes |
| Twitter/X — AI leaders | Model releases, framework updates, product launches |
| Twitter/X — PM thought leaders | Role evolution, hiring, workflow changes |

### Tier 2 — High signal

| Source | What to look for |
|--------|-----------------|
| r/fintech | Regulation shifts, AI in financial products, pain points |
| r/LangChain + r/LocalLLaMA | Framework updates, new patterns, community pain points |
| LinkedIn (AI PM space) | Job signals, content from hiring managers, industry moves |
| TLDR AI newsletter | Quick digest of the week's AI news |
| Lenny's Newsletter | PM craft, growth, and product strategy takes |

### Tier 3 — Contextual

| Source | What to look for |
|--------|-----------------|
| r/personalfinance | Unmet needs in personal finance — passive income idea signals |
| r/SideProject + r/indiehackers | What builders are shipping, what's getting traction |
| Product Hunt (week's top) | AI tool launches, what's resonating with early adopters |

---

## Key Twitter/X Accounts to Monitor

**AI / Technical:**
- @karpathy, @emollick, @swyx, @AnthropicAI, @OpenAI, @LangChainAI
- @rohanparekh, @GregBrockman, @sama

**PM / Product:**
- @lennysan, @shreyas, @cagan, @johncutlefish, @joulee

**Indie Builders / AI Products:**
- @levelsio, @bentossell, @danshipper, @jaredpalmer

---

## Scan Protocol

Claude should run a web search for each of the following queries (adapt as news evolves):

```
site:reddit.com/r/ProductManagement AI productivity [past week]
site:news.ycombinator.com AI product tools [past week]
site:reddit.com/r/fintech AI fintech tools [past week]
Twitter/X: AI PM productivity tools
latest AI agent frameworks release [past week]
new LLM tools for product managers [past week]
fintech AI innovation [past week]
```

---

## Output Format

Claude writes a new weekly entry to `Knowledge/learning-log.md` using the digest template:
`Templates/learning-digest.md`

---

## Backlog Translation Rules

After scanning, Claude should add tasks to `Tasks/backlog.md` under `## 🧠 Learning-Driven` if:

| Signal type | → Backlog action |
|-------------|-----------------|
| New tool that could accelerate builds | `Explore [tool] — try it on Probe or job search` [S] |
| Trend relevant to Probe positioning | `Research [trend] — update Probe PRD or pitch` [S] |
| Framework or pattern worth learning | `Learn [framework] — build a small experiment` [M] |
| Product idea triggered by a pain point | `Capture idea: [name] — open idea canvas` [S] |
| Job market signal | `Research [company/role] — add to target list` [S] |
| Insight worth publishing | `Write post: [angle] — LinkedIn or portfolio` [M] |

Only add tasks if they're genuinely actionable this or next sprint. Don't bloat the backlog.

---

## Time Budget

The full scan + digest + backlog update should take **~30–45 minutes**.
The remaining Sunday hour goes to sprint planning.
