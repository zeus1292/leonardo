# Idea Canvas: Proof of Build

**Date captured:** 2026-03-11
**Status:** Validated — needs 3 user conversations before building

---

## The Idea

**One sentence:** A structured portfolio platform for AI builders and AI PMs that proves competency with evidence — not just claims — optimized for time-pressed hiring managers.

**Problem it solves:** AI PMs and builders can't credibly prove their skills to recruiters. GitHub shows code but not product thinking. LinkedIn shows job titles but not evidence. There's no standardized, trusted way to say "here's proof I understand RAG, agentic systems, and AI evaluation" — with receipts.

**Who it's for:** AI PMs, ML engineers, and AI builders who are job searching or building credibility in the market. Specifically people who have done real work but struggle to communicate it to non-technical recruiters and time-pressed HMs.

**Why now / why AI:** AI can analyze your project descriptions and extract a structured skill map, compare it against a job description, and surface the gap — something no existing tool does. The AI PM role is also new enough that there's no established "proof standard" yet.

---

## Gut Check

- [x] I've personally felt this pain — actively navigating this with recruiters right now
- [ ] I know 3+ people who would pay today — **needs validation**
- [x] AI makes this meaningfully better — skill extraction, JD matching, gap analysis are only possible with AI

---

## Market

**Existing solutions:**
- GitHub — code only, no product thinking, HMs don't read it
- LinkedIn — claims only, no proof, no AI-specific structure
- Personal portfolio sites — unstructured, no recruiter UX
- Read.cv — design-focused, not adopted in AI/PM space
- Polywork — faded

**The wedge:** Standardized "project evidence cards" + AI-extracted skill map + recruiter-optimized public view. Nothing exists specifically for AI builders + PMs that speaks to both technical and product dimensions.

**Market size:** AI PM job market is growing fast. Broader TAM = any technical professional job searching (engineers, data scientists). Start narrow: AI PMs and builders.

**Competitors:** None directly in this niche. Indirect: all portfolio tools above.

---

## Monetization

**Model:** Freemium SaaS

**Free tier:** Profile + up to 3 project cards + public shareable link

**Paid ($15/mo):**
- Unlimited project cards
- AI skill extraction → structured skill map
- Job description gap analysis (paste a JD → see your skill match %)
- Recruiter analytics (who viewed, from where)
- Custom domain
- PDF export

**Path to first dollar:**
1. Akshay builds his own profile (he's user zero)
2. Posts about the build on LinkedIn
3. Someone DMs asking to join → charges $15 for early access

**Path to $1k MRR:** 67 paying users at $15/mo. Achievable via LinkedIn, Latent Space Discord, AI PM Slack communities.

---

## Build Plan

**MVP scope (2 weeks):**
- User auth (Clerk)
- Profile creation + project card builder (structured template)
- AI skill extraction from project descriptions (Claude API)
- Public shareable profile page (recruiter view)
- Basic Stripe integration for paid tier

**V2 (after first 10 paying users):**
- Job description matching + gap analysis
- Recruiter analytics dashboard
- Custom domain support

**Core technical risk:** AI skill extraction quality — needs to feel accurate and trustworthy, not just a buzzword list. Needs good prompt engineering and a clear schema for skill categorization.

**Stack:** Next.js, Postgres (Supabase), Claude API, Clerk, Stripe, Vercel

---

## Validation Score

| Dimension | Score (1-5) | Notes |
|-----------|-------------|-------|
| Pain strength | 5 | Living it. AI PM market is growing and underserved |
| Willingness to pay | 3 | Job seekers do pay, but $15/mo needs user conversation validation |
| Build simplicity | 3 | Doable solo in 2-3 weeks for V1 |
| Distribution path | 4 | LinkedIn, Latent Space, AI PM Slack — clear communities |
| **Total** | **15/20** | Move forward — validate willingness to pay first |

---

## Next Steps

- [ ] Talk to 3 AI PMs/builders: "Would you pay $15/mo for this while job searching?"
- [ ] Build Akshay's own profile as V0 (no product yet — just structured doc/page)
- [ ] Post about the problem on LinkedIn, gauge response
- [ ] If validation passes → create project folder in Projects/active/

---

## Key Questions to Answer Before Building

1. Will job seekers pay $15/mo, or do they expect this free?
2. Is the HM/recruiter view actually useful to that audience — or do they have their own tools?
3. Could there be a recruiter-side paid product (companies pay to access the pool) that makes the job seeker side free?

---

## Raw Notes

- Akshay is user zero — strongest possible distribution play is to build his own profile and document the journey publicly
- The "build in public" angle doubles as both validation and marketing
- Consider whether this stays a portfolio tool or evolves into a verified AI skills credential (longer-term)
- InvestorLens + Retail Right already exist as content — could be first project cards on the platform
- Idea B (Job Hunt Intel) could be a feature within this product eventually — the platform knows your skills, so it can match you to fresh roles
