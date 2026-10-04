# Market Research Report (v3): The AI Software Factory for Small Software Companies

**Topic:** Demand for, and feasibility of, an AI software factory: specs go in; planned, built, tested, secured, deployed and maintained software comes out, with evidence for every change.
**Target market:** Small software companies. That means solo technical founders, product teams of 1–20 engineers, and development agencies and freelancers.
**End goal:** The most trusted way for a small team to run a whole software company, because engineers stop typing code and start running factories.
**Date:** 2026-10-04 (v3; replaces the [OPC platform v2 report](../2026-09-26-opc-platform/market-research.md))
**Decisions applied:** all nine pivot decisions, approved 2026-10-04 ([pivot proposal §9](./pivot-proposal.md#9-decisions-for-you)).

**Companion documents:**
- [Factory lines: what the factory makes, line by line](./factory-lines.md)
- [The factory harness: reliability, safety and cost](./reliability-cost-harness.md)
- [Product feature strategy (CPO): bets, backlog and roadmap](./product-feature-strategy.md)
- [Product requirements document (PRD v2)](./prd.md)
- [Go-to-market and marketing plan](./marketing-plan.md)
- [X build-in-public guide](./x-build-in-public-guide.md)

**Method.** I used primary data wherever it exists:
- **Census:** Statistics of U.S. Businesses (SUSB) 2021 for firm counts by size, and Nonemployer Statistics 2023.
- **METR:** raw time-horizon data.
- **Google Trends.**
- **RDAP domain registries.**
- **Customer reviews:** 656 one- and two-star and 246 four- and five-star Trustpilot reviews of seven AI-coding products, rendered in a headless browser and coded by theme.
- **Developer discussion:** 2,129 first-person Hacker News comments about coding agents (July–October 2026), coded by theme.
- **Prices:** the Claude API price list.
- **Feasibility:** a capability inventory of this repository (Paperclip).

Secondary data (press, aggregators) is labeled as such. See [Data quality notes](#data-quality-notes).

---

## Executive Summary

**Verdict: Go, with a sharp target.** Demand for AI software development is enormous and already paid for. Most of the money and competition sits with large enterprises and with non-technical "prompt to app" buyers. The open ground is a **governed, end-to-end factory for small software companies**, competing on **verified outcomes, safety and predictable economics**, not on having the best coding model.

1. **Demand is proven at a scale few software markets have reached.**
   - **90%** of professional developers use AI coding agents at work every week, and 68% daily (JetBrains, 15,000+ developers, mid-2026).
   - Revenue leaders:
     - Cursor passed **$4B** in annualized revenue and was bought by SpaceX for **$60B**.
     - Claude Code passed a **$2.5B** run rate in February 2026.
     - Cognition is near **$900M** at a **$48B** valuation.
     - Lovable is valued at **$13.3B** and Replit at **$9B**.
   - Gartner launched a standalone "Enterprise AI Coding Agents" Magic Quadrant in May 2026.
2. **The bottleneck has moved from writing code to verifying, securing and paying for it.**
   - AI-authored pull requests carry about **1.7x** more issues.
   - The security pass rate of AI-generated code is stuck at **56%**.
   - Developers can fully delegate only **0–20%** of tasks.
   - Review is now the most discussed coding-agent topic on Hacker News (24% of first-person comments), ahead of cost (17%).
   - Token bills are breaking budgets: Uber spent its 2026 AI budget in four months.
3. **Capability compounds fast, so the factory must be designed to grow into autonomy.**
   - METR's best measured agent finishes about **3.1 hours** of expert work 80% of the time, and about **17 hours** 50% of the time.
   - The fitted doubling time is about **129 days**.
   - The factory therefore splits work into orders that agents can finish reliably today, and enlarges them automatically as measured pass rates rise.
4. **Small software companies are numerous, paying and underserved by a governed factory.**
   - The US has about **220K core accounts**:
     - 95.6K IT and software freelancers earning ≥ $50K;
     - 113.9K computer-systems-design firms with under 20 employees;
     - 10.2K small software publishers.
   - Solo founders formed **63%** of Stripe Atlas C corporations in Q2 2026.
   - Enterprise factories (8090 at $200 per user plus tokens; Factory) sell top-down. App builders (Lovable, Replit) sell prototypes to non-engineers.
5. **What customers hate is the economics, not the AI.**
   - **66%** of negative reviews of AI-coding products complain about money: 49% about credits and usage, 42% about billing and refunds.
   - **39%** complain about support.
   - **24%** say they paid for the tool's own failures.
   - "Failed work is free," a price known before work starts, and humans who answer are the cheapest strong differentiators available. They carry over directly from our OPC work.
6. **Feasibility is high, because we build on Paperclip.** This MIT-licensed repository already has most of a factory control plane:
   - issues and plan decompositions;
   - 12 coding-agent adapters;
   - 8 sandbox providers;
   - execution workspaces;
   - managed GitHub identity, plus GitHub review checks and pull-request merge state;
   - low-trust containment;
   - approvals, budgets, completion contracts and evals.
   
   The beta P0 is about **80 person-weeks** on Paperclip (69 of engineering, plus design, security and QA), against about 145 from scratch.
7. **Economics work with outcome pricing.**
   - A Medium change (1–3 hours of human work) costs about **$5** in models plus sandbox.
   - Priced at **$12 per merged change**, it earns about 50% gross margin even after paying for failed attempts.
   - A small platform fee per workspace and an optional bring-your-own-key mode cover power users and agencies.

### Scorecard

| Dimension | Rating | Evidence |
|---|---|---|
| Market demand | **Very strong** | 90% weekly agent use; multi-billion-dollar run rates; Gartner category |
| Willingness to pay | **Proven at $20–200 per seat; enterprises spend $150–2,000 per engineer per month on tokens** | Claude, Cursor, Copilot, Devin, Factory price ladders (§4.2); Claude Code enterprise average; Uber |
| "AI software factory" as positioning | **Good as a category, unavailable as a brand** | Search interest up about 4x since Q1 2025 but small; "Factory" is Factory.ai's brand; "Software Factory" is 8090's product name |
| Technical feasibility | **High** | Paperclip already covers most of the control plane (§6.1) |
| Reliability at acceptable cost | **Medium → High with the factory harness** | Order sizing to METR's reliable horizon; executable definitions of done; holdout scenarios; about $5 per Medium change |
| Competitive intensity | **Extreme** | Labs, platforms and seven funded start-ups; consolidation (Cursor–Graphite, Cognition–Windsurf, SpaceX–Cursor) |
| Regulatory and reputational risk | **Medium** | Security incidents (PocketOS, data-leaking vibe-coded apps); EU Cyber Resilience Act; copyright of AI-only code; "replace engineers" backlash |

---

## What changed since v2 (the OPC report)

| Item | v2: OPC platform | v3: software factory |
|---|---|---|
| Customer | Solo service businesses (consultants, coaches, creators, designers, property agents) | Small software companies: solo technical founders, teams ≤ 20, agencies and freelancers |
| Job | Run the front office, revenue loop and content | Plan, build, verify, release and operate software |
| Category | "The platform for one-person companies" | "AI software factory." "One-person software company" is used only to describe the audience |
| Revenue per account | About $65 a month | About $200–1,000 a month |
| Core US accounts | 1.63M (13 segments ≥ $50K) | About 220K |
| Biggest platform risk | Google restricted-scope verification (CASA) for Gmail | Labs and platforms bundling factory features; token-cost volatility |
| Foundation | From scratch (PRD v1) | **Paperclip fork** (decision D4) |
| Launch | Public beta, Consultant + Coach kits, week of 25 Jan 2027 | Public beta, **Bug + Maintenance lines with a Feature-line preview**, same week (D7) |

The OPC research is kept, unchanged, in [`../2026-09-26-opc-platform/`](../2026-09-26-opc-platform/README.md). Its Census segment data is reused here for freelancers (§3.1).

---

## 1. Market Overview

### 1.1 From coding assistants to software factories

Dan Shapiro's five levels have become the industry's shorthand ([Simon Willison](https://simonwillison.net/2026/Jan/28/the-five-levels/)):

| Level | Name | Human role | Typical tools today |
|---|---|---|---|
| 0 | Spicy autocomplete | Writes everything | Early Copilot |
| 1 | Coding intern | Reviews all output | Chat assistants |
| 2 | Junior developer | Pairs, reviews every line | IDE agents |
| 3 | Developer | Full-time reviewer of AI code | Claude Code, Codex, Cursor agents |
| 4 | Engineering team | Writes specs and plans; agents do the work | Background agents, Devin, Factory, 8090 |
| 5 | Dark software factory | Writes specs; a black box ships software | StrongDM's internal factory (3 engineers; "code must not be written or reviewed by humans") |

**Definition used in this document.** An *AI software factory* is a governed system in which agents carry work through every stage (spec → plan → build → verify → release → operate). Three things set it apart from a coding agent:
1. every change carries evidence that it met its definition of done;
2. agents can't harm production by design;
3. humans step in where risk requires it.

[StrongDM's write-up](https://simonwillison.net/2026/Feb/7/software-factory/) is the clearest public example of how to check work without human review: holdout scenarios stored outside the codebase, a probabilistic "satisfaction" score, and clones of third-party services (a "Digital Twin Universe").

### 1.2 Money in the market

| Company | What it sells | Scale signal | Source |
|---|---|---|---|
| Cursor (SpaceX) | IDE plus agents; Graphite code review | $4B+ annualized revenue (Jun 2026); acquired for $60B (closed 14 Aug 2026) | [CNBC](https://www.cnbc.com/2026/06/16/spacex-spcx-cursor-acquisition-ipo.html), [Dealroom](https://dealroom.co/news/134107-cursor-tops-4b-annualized-revenue/) |
| Anthropic: Claude Code | Agentic coding (CLI, IDE, web); Code Review; Managed Agents | Run rate above $2.5B (12 Feb 2026); used by 39% of developers | [VentureBeat](https://venturebeat.com/technology/anthropic-says-it-hit-a-30-billion-revenue-run-rate-after-crazy-80x-growth), [JetBrains](https://blog.jetbrains.com/research/2026/08/ai-coding-agent-adoption-2026/) |
| OpenAI: Codex | Coding agent in ChatGPT and CLI | Gartner Leader; about 5M weekly users (Jun 2026, reported) | [OpenAI](https://openai.com/index/gartner-2026-agentic-coding-leader/), [Constellation (secondary)](https://www.constellationr.com/insights/news/openai-touts-broadening-codex-usage-5-million-weekly-active-users) |
| GitHub Copilot and Agent HQ | Assistant plus a multi-vendor agent "mission control" | 4.7M paid subscribers, up 75% year over year (Jan 2026) | [Microsoft](https://www.microsoft.com/en-us/investor/events/fy-2026/earnings-fy-2026-q2), [GitHub](https://github.blog/news-insights/company-news/welcome-home-agents/) |
| Cognition (Devin + Windsurf) | Autonomous engineer plus IDE | Run rate about $900M; $2B raised at $48B (Sep 2026) | [Bloomberg](https://www.bloomberg.com/news/articles/2026-09-08/ai-startup-cognition-raises-2-billion-at-a-48-billion-value) |
| Factory | "Droids" across the lifecycle: review, security, QA, docs, incident response | $200M at $5B (Sep 2026); Nvidia, Adobe, Palo Alto Networks | [DevOps.com](https://devops.com/factory-raises-200m-as-it-builds-agents-across-the-software-lifecycle/) |
| 8090 | "Software Factory": Requirements, Blueprints, Work Orders, Tests, Feedback | $135M Series A; EY deployment | [Ry Walker](https://rywalker.com/research/8090-software-factory), [EY](https://www.ey.com/en_us/newsroom/2026/03/ernst-young-llp-and-8090-launch-ey-ai-pdlc) |
| Lovable | Prompt-to-app for non-engineers, moving into "running businesses" | $400M at $13.3B (Aug 2026); 60M+ projects | [Lovable](https://lovable.dev/blog/series-c) |
| Replit | Agent plus hosting | About $525M annualized revenue (Apr 2026); $9B | [Sacra](https://sacra.com/c/replit/) |
| AWS | Kiro, plus Security and DevOps "frontier agents" (generally available 31 Mar 2026) | — | [AWS](https://aws.amazon.com/blogs/machine-learning/aws-launches-frontier-agents-for-security-testing-and-cloud-operations/) |
| Google | Antigravity 2.0 (agent teams), Jules | Free for individuals in preview | [Antigravity](https://antigravity.google/) |
| Point tools | Review (CodeRabbit, Greptile), SRE (Resolve AI at $1B+, Traversal), security (Snyk, Semgrep) | Resolve AI: $125M at $1B (Feb 2026) | [Bloomberg](https://www.bloomberg.com/news/articles/2026-02-04/resolve-ai-hits-1-billion-valuation-for-outage-thwarting-ai-agents) |

**Reading:**
- The coding-agent layer is owned by labs and platforms. They ship at model cost and own distribution.
- Start-ups that win either go all-in on enterprise (Cognition, Factory, 8090) or on non-engineers (Lovable, Replit).
- Nobody has made the *governed factory for small teams* their main product.

### 1.3 Adoption

| Signal | Number | Source |
|---|---|---|
| Weekly / daily use of AI coding agents at work | 90% / 68% | [JetBrains, 15K+ developers, May–Jul 2026](https://blog.jetbrains.com/research/2026/08/ai-coding-agent-adoption-2026/) |
| Main tool | Claude Code is the main tool for 31%; overall use: Claude Code 39%, Copilot 21%, Codex 16%, Cursor 12% | Same |
| Developers using or planning to use AI tools | 84%. But trust in accuracy is 29% and active distrust is 46% | [Stack Overflow 2025 survey](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/) |
| AI use vs full delegation | About 60% of work uses AI; 0–20% of tasks are fully delegated | [Anthropic 2026 Agentic Coding Trends Report](https://resources.anthropic.com/2026-agentic-coding-trends-report) |
| Code output per engineer at Anthropic | Up about 200% in a year, which made review the bottleneck | [VKTR](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/) |

### 1.4 The capability trend (METR raw data, pulled 2026-10-04)

| Model (release) | 50% horizon | 80% horizon |
|---|---|---|
| o3 (Apr 2025) | 2.0 h | 30 min |
| GPT-5 (Aug 2025) | 3.4 h | 38 min |
| Claude Opus 4.5 (Nov 2025) | 4.9 h | 49 min |
| Claude Opus 4.6 (Feb 2026) | 12.0 h | 70 min |
| Gemini 3.1 Pro (Feb 2026) | 6.4 h | 90 min |
| Claude Mythos Preview, early (Apr 2026) | **17.4 h** | **3.1 h** |

The **horizon** is the length of task, in expert-human time, that an agent completes with the given probability. METR's fitted doubling time since 2023 is **about 129 days** (95% CI 104–158 days) ([METR](https://metr.org/time-horizons/)). If the trend holds, the reliable (80%) horizon grows about 7x a year. METR notes that measurements above about 16 hours are unreliable with its current task suite.

**What it means for the product:**
1. Size work orders to what agents finish reliably **on this repository**, not to the headline 50% horizon.
2. Measure pass rates per repository and per factory line.
3. Let order size and autonomy grow automatically as the evidence improves. That is how a factory moves from Level 4 to Level 5 without a leap of faith.

### 1.5 The new bottleneck: verification, safety and cost

| Finding | Source |
|---|---|
| AI raises delivery throughput **and** instability: more change failures, rework and time to recover. It amplifies whatever testing and platform maturity a team already has | [DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/) |
| AI-authored PRs: 10.83 issues per PR vs 6.45 for humans (about 1.7x); logic issues +75%; security issues up to 2.74x | [CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report) |
| Security pass rate of AI-generated code is flat at 56% across 100+ models | [Veracode 2026](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/) |
| An agent deleted a production database and all its backups in 9 seconds (PocketOS, 25 Apr 2026). The causes were an over-privileged CLI token found in an unrelated file, shared blast radius and no gate on destructive actions | [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/claude-powered-ai-coding-agent-deletes-entire-company-database-in-9-seconds-backups-zapped-after-cursor-tool-powered-by-anthropics-claude-goes-rogue) |
| About 5,000 apps built with vibe-coding tools were leaking sensitive data (RedAccess, May 2026). 2,038 critical vulnerabilities and 400+ leaked secrets were found across 1,400 such apps (Escape) | [CSA research note](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/) |
| Claude Code enterprise average: about $13 per active developer-day, $150–250 per developer per month | [Claude Code docs](https://code.claude.com/docs/en/costs) |
| Uber spent its 2026 AI budget in four months; power users cost $500–2,000 per engineer per month; it then capped spend | [Forbes](https://www.forbes.com/sites/janakirammsv/2026/05/17/uber-burns-its-2026-ai-budget-in-four-months-on-claude-code/) |
| GitHub Copilot's switch to usage-based billing (1 Jun 2026) drew a backlash over quotas used up in hours | [The Register](https://www.theregister.com/ai-and-ml/2026/06/02/github-copilot-users-threaten-exit-as-metered-billing-kicks-in/5249826) |

### 1.6 Market sizing (order of magnitude; assumptions stated)

| Layer | Estimate | Basis |
|---|---|---|
| **Labor pool being reshaped** | ≈ **$255B a year** (US) | 1,905,400 software developer, QA and tester jobs × $134,040 median pay ([BLS](https://www.bls.gov/ooh/computer-and-information-technology/software-developers.htm)). Worldwide there are 47.2M developers, 36.5M of them professional ([SlashData](https://www.slashdata.co/post/global-developer-population-trends-2025-how-many-developers-are-there)) |
| **Tool spend (TAM proxy)** | ≈ **$10B** (2026) enterprise AI coding agents; the top three vendors alone exceed $7B in run rate | Gartner, reported ([Enterprise DNA, secondary](https://enterprisedna.co/resources/news/gartner-enterprise-ai-coding-agents-10-billion-market-2026/)); §1.2 |
| **SAM: small software companies, US** | ≈ **$0.5–2.6B a year** | About 220K core accounts (§3.1) × $200–1,000 a month |
| **SAM: global** | ≈ $2–10B a year | Assumes the US is 20–25% of small-team spend. Validate with the Phase 0 pricing data |
| **SOM: 3 years** | ≈ **$20–40M ARR** | 1–2% of US core accounts at about $400 a month (2.2–4.4K accounts), plus a similar amount internationally |

**Sensitivity.** The SOM moves most with *revenue per account*. If factories really take over engineering labor, spend per account rises toward the $500–2,000 per engineer per month that heavy enterprise users already pay. Upside also comes from moving up-market (§8, Phase 3).

---

## 2. Positioning: is "AI software factory" feasible?

### 2.1 Search demand (Google Trends, worldwide, quarterly averages on a shared 0–100 scale; pulled 2026-10-04)

| Term | Q1 2025 | Q3 2025 | Q1 2026 | Q2 2026 | Q3 2026 |
|---|---|---|---|---|---|
| software factory | 4.8 | 14.1 | 22.6 | 31.2 | 20.7 |
| AI software factory | 0.0 | 2.2 | 3.8 | 6.1 | 3.4 |
| dark factory | 3.1 | 6.5 | 12.5 | 18.4 | 8.3 |
| vibe coding | 11.5 | 43.9 | 65.1 | 68.1 | 49.5 |
| AI coding agent | 0.9 | 6.2 | 21.2 | 72.4 | 30.7 |

- In a second pull, "Claude Code" ran about **13–18x** "vibe coding." So "software factory" is about 3% of "Claude Code."
- "Software factory" is also ambiguous: US defense software factories and manufacturing software both use it.
- Every term dipped in Q3 2026, as they did in the September pull, so treat that as sampling noise rather than a reversal.

**Reading:** the term is rising and has a clear meaning to engineers who follow the field (Shapiro's levels, StrongDM, 8090, Factory). It's not yet a mass search term. Use it as the **category** in content, PR and SEO. Win search on jobs to be done ("fix bugs automatically," "upgrade dependencies automatically," "AI code review with tests").

### 2.2 Naming, trademarks and domains

| Item | Finding | Implication |
|---|---|---|
| "Factory" | Factory.ai's brand ($5B company) | Never use "Factory" alone, or as the lead word of our brand |
| "Software Factory" | 8090's product name; also a generic US defense term | Use it as a descriptive category phrase only ("an AI software factory") |
| "Dark factory" | Industry term for Level 5 (Shapiro) | Good in content; poor as a brand (it sounds ominous) |
| Short compound domains | RDAP, 2026-10-04: all 12 candidate `.com` names were registered (for example specline, shipline, linewright, mergewright, provenline, factoryofone, verifyline). `.dev` versions were free for 8 of 12 (for example linewright.dev, mergewright.dev, provenline.dev, factoryofone.dev) | Plan for a coined name, or a `.dev` / `.ai` domain plus a `get…` / `use…` `.com`. Run a USPTO and EUIPO knock-out search on 3 finalists |
| "One Person Company" | OPC Foundation marks; generic phrase (see v2) | Audience phrase only: "the factory for one-person software companies" |

### 2.3 Recommendation

- **Category:** "AI software factory."
- **Promise:** "Specs in. Verified, shipped software out."
- **Audience line:** "Run a whole software company with a team of one."
- **Belief (founder voice, not product claim):** "Engineers stop typing code and start running factories."

Avoid "replace engineers" in product copy, ads and launch materials, for three reasons:
1. our champions are engineers;
2. the hiring data doesn't support it yet (Indeed: 71% of the year's growth in software-development postings came from senior roles, [Hiring Lab](https://hiringlab.indeed.com/2026/07/08/ai-and-job-postings-from-destruction-to-creation/));
3. productivity and replacement claims need substantiation (FTC).

---

## 3. Target Market

### 3.1 US segment sizing (Census; primary data)

| Segment | Source | Count | Notes |
|---|---|---|---|
| IT and software freelancers (nonemployers, NAICS 5415) | NES 2023 | 343,329 | **95,641 (28%) earn ≥ $50K**. Average receipts are $60.0K |
| Computer-systems-design firms with under 20 employees (NAICS 5415) | SUSB 2021 | **113,874** firms, 310,035 employees | Includes 56,309 custom-programming shops (541511) and 44,078 systems-design firms (541512) |
| Software publishers with under 20 employees (NAICS 511210) | SUSB 2021 | **10,231** firms, 38,594 employees | 7,278 have fewer than 5 employees |
| **Core accounts** | — | **≈ 220K** | 95.6K + 113.9K + 10.2K |
| Solo-founder momentum (not additive) | Carta, Stripe | 36% of Carta startups (2025); **63% of Atlas C corporations (Q2 2026)** | AI-native solo startups make about 2x the revenue of other solo startups by year two ([Stripe](https://stripe.com/blog/top-solo-founder-traits)) |

The count is conservative. Technical founders of SaaS companies often register under other industry codes, and international demand is excluded.

### 3.2 Who to serve first

Each sub-segment is scored 1–5 on each criterion:

| Sub-segment | Pain | Ability to pay | Speed of decision | Reach via build-in-public | Verifiable work | Word of mouth | Total |
|---|---|---|---|---|---|---|---|
| **Agencies and freelancers** | 5 | 4 | 5 | 3 | 4 | 4 | **25** |
| **Solo technical founders** | 5 | 3 | 5 | 5 | 3 | 5 | **26** |
| Small product teams (2–20) | 4 | 5 | 3 | 3 | 4 | 3 | 22 |
| Non-technical founders | 4 | 2 | 4 | 4 | 2 | 3 | 19 |

**Sequence:**
1. **Solo technical founders and agencies/freelancers** at public beta (W0, week of 25 Jan 2027).
2. **Small teams** at GA (late April 2027), with the Team plan, SSO-lite and review routing.
3. **Non-technical founders** only through agencies (the Agency line), not directly.

### 3.3 Primary personas

| Persona | Snapshot | Jobs to be done | Success looks like |
|---|---|---|---|
| **Sam, solo technical founder** | 34; one B2B SaaS at $8K MRR; Next.js + Postgres; maintains everything alone | Ship the roadmap; keep dependencies and security current; fix bugs before customers notice | A feature a week without nights; zero "2 a.m." incidents; costs he can predict |
| **Ines, agency owner** | 41; 6 people; 12 client repositories; fixed-price projects | More delivered per person; consistent quality; client handovers | 30% more projects with the same team; fewer post-launch defects |
| **Raj, startup CTO** | 38; 8 engineers; Series A | Ship faster without hiring; keep review and security sane | Throughput up, change-failure rate flat or down |
| **Dana, freelance developer** | 29; bills by project | Finish fixed-price work faster at provable quality | Double the projects; evidence to show clients |

### 3.4 What they struggle with today (two voice-of-customer sources)

**Hacker News**
- **Sample:** 2,129 first-person comments mentioning coding agents, July–October 2026 (median late September).
- **Coding:** keyword-coded by theme; one comment can have several themes. These are discussion topics, not only complaints.

| Theme | Share of comments |
|---|---|
| **Review burden** (reading and reviewing AI code and PRs) | **24.4%** |
| Cost, limits, pricing | 17.4% |
| Context and large codebases | 16.8% |
| Tests and verification | 15.4% |
| Wrong, "almost right," regressions | 14.0% |
| Maintainability and "slop" | 12.9% |
| Productivity gains | 10.6% |
| Security and destructive actions | 9.8% |
| Jobs and skills | 9.5% |
| Specs and planning | 7.4% |
| Trust and oversight ("babysitting") | 6.1% |
| Parallel agents and orchestration | 5.1% |

**Trustpilot** (656 negative reviews; §4.4): money 66%, support 39%, bugs and loops 32%, paid for failure 24%.

**Combined reading:**
- Engineers worry most about **reviewing and verifying** output and about **cost**.
- Buyers of app builders are angriest about **money and support**.
- Our factory is designed to answer both with:
  - evidence-first review;
  - an executable definition of done;
  - outcome pricing;
  - human support.

---

## 4. Competitive Landscape (verified 2026-10-04)

### 4.1 Segment map

| Segment | Main players | Buyer | Pricing model | What they leave open for small teams |
|---|---|---|---|---|
| Coding agents (labs) | Claude Code, Codex, Gemini / Antigravity | Individual developers, enterprises | Subscriptions with usage windows; API tokens | An end-to-end factory with evidence; per-outcome pricing; model neutrality |
| Platforms and IDEs | GitHub Copilot + Agent HQ, Cursor, Windsurf | Developers, IT | Seats plus credits or usage | Verification and release governance; predictable bills (Copilot backlash) |
| Autonomous engineers | Devin | Teams, enterprises | Compute units (about $2.25 per 15 min on Core) | Price known before work; failed work free |
| Enterprise factories | Factory, 8090, AWS frontier agents | Enterprise engineering | Seats plus tokens; $1M+ deals (8090) | Self-serve for 1–20 engineers |
| App builders | Lovable, Replit, Bolt, Base44, Emergent | Non-engineers, founders | Credits | Production-grade verification, maintenance, fair billing (§4.4) |
| Point tools | CodeRabbit, Graphite, Greptile; Snyk, Semgrep; Resolve AI, Traversal | Teams | Seats or usage | One loop from spec to operate |
| Orchestration | Paperclip (open source), Agent HQ, small orchestrators | Developers | Free or seats | Productized lines, verification, a factory UX for non-specialists |

### 4.2 Price baseline (list prices, October 2026)

| Product | Entry | Power / team | Notes |
|---|---|---|---|
| Claude (Claude Code included) | Pro $20 / month | Max $100 or $200; Team Premium about $125–150 per seat | [Secondary summary](https://intuitionlabs.ai/articles/claude-pricing-plans-api-costs) |
| Cursor | Pro $20 | Pro+ $60, Ultra $200; Teams $40 per user | [DEV summary](https://dev.to/rahulxsingh/cursor-pricing-in-2026-hobby-pro-pro-ultra-teams-and-enterprise-plans-explained-4b89) |
| GitHub Copilot | Pro $10 | Pro+ $39; Business $19, Enterprise $39 per user; usage-based AI Credits since 1 Jun 2026 | [GitHub](https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/) |
| Devin | Core $20 plus $2.25 per compute unit | Team $500 / month (250 units) | [Secondary](https://www.usecarly.com/blog/devin-pricing/) |
| Factory | Pro $20 | Plus $100, Max $200 (rolling rate limits) | [Secondary](https://continuumcode.ai/guides/factory-ai-pricing/) |
| 8090 Software Factory | $200 per user per month, tokens separate | Enterprise from $1M a year | [Ry Walker](https://rywalker.com/research/8090-software-factory) |
| Lovable | Pro $25 (100 credits) | Teams | [Secondary](https://www.eesel.ai/blog/lovable-pricing) |
| Replit | Core $20–25 (includes $20 of usage) | Pro, Enterprise | [Secondary](https://www.lowcode.agency/blog/replit-pricing-explained) |

**Reading:**
- Seat prices cluster at $20–200 per month, but **effective spend is driven by usage**: enterprise Claude Code averages $150–250 per developer per month, and heavy users pay $500–2,000.
- No leading product prices **per verified outcome**.

### 4.3 The six gaps

1. **Evidence gap.** Agents hand over code; the human verifies. Nobody ships "every change proven against its definition of done" as the main product for small teams.
2. **Safety gap.** Agents often run with the developer's own credentials. Production access, destructive commands and secrets are guarded by convention, not by the system's construction.
3. **Economics gap.** Credits, compute units and token meters make bills unpredictable, and customers pay for failed attempts.
4. **Operations gap.** Coding tools stop at the PR. Release, monitoring and fixing what shipped sit in separate tools.
5. **Small-team gap.** Enterprise factories sell top-down. App builders target non-engineers. Teams of 1–20 have no platform team to build the guardrails DORA says AI needs.
6. **Neutrality gap.** Lab and platform tools favor their own models. Small teams want the best model per job, and their choice of provider.

### 4.4 Voice of customer: 656 negative reviews (Trustpilot)

| Product | Trustpilot score (reviews) |
|---|---|
| Lovable | 4.2 (1,758) |
| Replit | 2.8 (1,555) |
| Base44 | 2.8 (898) |
| Emergent | 2.8 (636) |
| Bolt.new | 1.6 (203) |
| Cursor | 1.5 (337) |
| Windsurf | 1.4 (59) |

| Theme (1–2★, August 2025 to October 2026) | Share | Highest |
|---|---|---|
| **Any money issue** | **65.7%** | — |
| Credits and usage burn | 48.6% | Emergent 60%, Windsurf 55% |
| Billing, refunds, cancellation | 41.6% | Cursor 67%, Replit 54% |
| Support unresponsive or unhelpful | 39.3% | Emergent 53%, Cursor 50% |
| Bugs, loops, "fixes one thing, breaks another" | 31.9% | Emergent 42%, Replit 40% |
| **Paid for failure** | **24.4%** | — |
| "Scam" or "misleading" language | 17.5% | Emergent 27%, Replit 24% |
| Quality got worse | 11.9% | Cursor 22% |
| Deployment and production problems | 9.9% | Emergent 19% |
| Destructive changes, lost work | 8.1% | Base44 12%, Cursor 11% |

**What the positive reviews say (246, 4–5★):**
- 31% praise support;
- 23% mention speed;
- 18% mention ease;
- 15% mention a real business or app launched.

**Comparison with the OPC research:** that research found billing 53%, support 40% and credits 37%. **The pattern holds across categories: fairness and humans beat raw AI quality.**

---

## 5. Opportunities

Ranked by size × fit × defensibility:

1. **Verified changes as the unit of value.**
   - Every merged change carries an evidence card: the checks, holdout scenarios, scans and preview.
   - Price per merged change; failed work is free.
   - This addresses the evidence gap and the economics gap together.
2. **Safe by construction.**
   - Sandboxes only, with no production credentials.
   - A gate on destructive actions; twin services for third-party APIs.
   - "The factory that cannot delete your database" is a story people will repeat.
3. **Maintenance on autopilot** (Bug + Maintenance lines).
   - The easiest work to verify and the first "lights-out" candidate.
   - It answers the solo founder's biggest fear.
4. **The agency factory.** Separate client workspaces, per-client cost reports and handover packs. Agencies are paid per delivery, so throughput turns straight into margin.
5. **Operate what you ship.**
   - Release behind flags, monitor, roll back.
   - Incidents come back to the factory as new orders.
6. **Open line format plus a public factory benchmark.**
   - Category creation and the community flywheel.
   - Publish cost per verified change and failure rates.
7. **Model neutrality and bring-your-own-key.** Route each step to the best model; let power users bring their own keys.

---

## 6. Feasibility

### 6.1 Technical: High (Paperclip fork for the control plane; decision D4)

| Factory need | Already in Paperclip | Gap to build |
|---|---|---|
| Work orders, breakdown, dependencies | Issues, sub-issues, blockers, `issue_plan_decompositions` ([execution semantics](../../execution-semantics.md)) | Planner that sizes orders to measured pass rates |
| Many agents, model-neutral | 12 adapters (Claude Code, Codex, Cursor local/cloud, Gemini, OpenCode, Grok, Kimi, Pi, Hermes, OpenClaw) | Per-step routing policy |
| Isolated execution | Execution and project workspaces; runtime leases; **8 sandbox providers** (Cloudflare, CreateOS, Daytona, E2B, exe.dev, Kubernetes, Modal, Novita); execution allowlist that forces untrusted tenants into sandboxes | Factory-standard sandbox images per line; twin services |
| Safe GitHub access | Managed token-free `git`/`gh` launchers bound to the run's accepted identity ([doc](../../execution-github-identity.md)); GitHub review checks and PR reviews; PR merge-state resolution | Branch protections and auto-merge policy per risk tier |
| Hostile input | `low_trust_review` preset; containment; secret redaction in runs ([doc](../../LOW-TRUST-PRESETS.md)) | Injection red-team suite for issue text and dependency diffs |
| Approvals, budgets, audit | Approvals, decision queues, budget policies and incidents, cost events, quota windows, activity log | Evidence-first review inbox UX; outcome-priced usage ledger |
| Definition of done | `completion_contracts`, `work_assessments` | Executable checks library for code (tests, scans, scenarios, preview) |
| Recurring work | Routines, task watchdog | Maintenance line schedules |
| Deploy targets | Vercel connect, Railway services | Preview environments, flags, rollback adapters |
| Evals | Runner evals and product end-to-end evals ([doc](../../evals.md)) | Factory benchmark; per-line golden sets |

**Effort:** the beta P0 is about **80 person-weeks** on Paperclip (69 of engineering, plus about 11 of design, security and QA), against about 145 from scratch. The pivot proposal's earlier 60–75 range covered engineering only. Details are in the [PRD §18](./prd.md#18-delivery-plan).

**Main technical risks:**
- upstream churn (mitigated by a thin fork and contributing upstream);
- reliability on unfamiliar codebases (mitigated by order sizing and test-first orders);
- sandbox cost at scale (E2B and Daytona list at $0.0504 per vCPU-hour plus $0.0162 per GiB-hour, so a 2 vCPU / 4 GiB sandbox is about **$0.17 an hour**; [Northflank comparison](https://northflank.com/blog/ai-sandbox-pricing)).

### 6.2 Unit economics: viable with outcome pricing

**Model:** list prices from the [Claude API pricing](https://platform.claude.com/docs/en/about-claude/pricing) page:
- Sonnet 5.5: $2 input / $10 output per million tokens; $0.20 cache read.
- Opus 5.5: $4 / $20; $0.20 cache read.
- Haiku 4.5: $1 / $5.
- Sandbox: about $0.17 an hour.

| Change size | Work | Modeled cost |
|---|---|---|
| Small (≤ 30 min of human work) | Haiku triage, Sonnet build, light review | $1–2 |
| **Medium (1–3 h)** | Opus plan ≈ $0.60 · Sonnet build ≈ $2.50 · review agents ≈ $0.90 · sandbox and CI ≈ $0.15 · 30% revision allowance ≈ $0.75 | **≈ $5** |
| Large (> 3 h) | Split by the planner into Medium orders | Sum of the parts |

**Cross-check:** Anthropic's enterprise average of about $13 per active developer-day, at 2–4 changes a day, is about $3–6 per change. A human doing a Medium change at the BLS median wage, with about 30% overhead, costs about **$250–340**.

**Margin at $12 per Medium change:**

| Item | Amount |
|---|---|
| Model and sandbox cost | $5.00 |
| Failed-attempt overhead (25% failure rate × about $3 per failed order ÷ 0.75 merged) | ≈ $1.00 |
| **Gross margin per merged change** | ≈ **50%** |
| Gross margin on the platform fee | ≈ 90% |
| **Blended gross margin** | ≈ **55–60%** |

### 6.3 Pricing recommendation (decision D5; to validate in Phase 0)

There are two billing modes.
- **Managed (default):** a platform fee plus a **fixed price per merged change**, quoted before work starts. Failed or abandoned orders cost nothing. You set a hard monthly cap.
- **Bring your own key:**
  - a higher platform fee and no per-change fee;
  - you pay your model provider directly, at zero markup;
  - per-order budget caps still apply.

| Plan | Who | Managed | Bring your own key | Includes |
|---|---|---|---|---|
| **Solo** | Solo founders, freelancers | $29 / month + per change | $79 / month | 1 seat, 3 repositories, lines L1–L4 |
| **Team** (GA) | Teams of 2–20 | $199 / month (up to 5 seats; +$29 per extra seat) + per change | $399 / month | Review routing, policies, SSO-lite |
| **Agency** | Agencies | $399 / month (10 seats, unlimited client workspaces) + per change | $799 / month | Client workspaces, per-client cost reports, handover packs (L5) |
| **Per change (Managed)** | — | **Small $3 · Medium $12** | — | Large orders are split into Medium ones; the price is shown before you approve the order |
| **Trial** | — | 14 days, no card, **10 free Medium changes** | — | — |
| **Founding members** | First 500 accounts | 40% off the platform fee for year one | — | — |

**Always included:**
- failed orders are free;
- a hard monthly cap that you set;
- the cost shown on every change card;
- one-click cancel and pause;
- a human support reply within 1 business hour on Team and Agency plans (4 hours on Solo).

**Example bills:**
- Solo founder, 30 Medium changes a month: about **$389**.
- Team, 80 changes: about **$1,159**.
- Agency, 150 changes: about **$2,199**.

These fit the $200–1,000 per account range used in sizing (agencies run above it).

### 6.4 Product and UX: a factory floor, not an agent zoo

- **What users see:** orders, lines, evidence cards, releases, cost and a weekly factory report.
- **What they never see:** heartbeats, adapters, org charts or token counts. Cost appears in dollars per change.
- **Zero-prompt start:** connect a repository → **Repo X-ray** (test gaps, vulnerable dependencies, flaky tests, missing CI, open bugs) → five suggested orders → first merged change in ≤ 30 minutes.
- **One inbox,** sorted by risk tier:
  - Low tier merges automatically once trusted;
  - Medium is approved in batches;
  - High is approved individually, and never automatically.
- **Autonomy is earned:**
  - each line shows its track record (first-pass merge rate, false-green rate, change-failure rate);
  - promotion to lights-out is suggested only on evidence.

---

## 7. Risks and Challenges

| Risk | Impact | Likelihood | Mitigation |
|---|---|---|---|
| Labs and platforms bundle factory features at model cost (Agent HQ, Claude Code, Codex, Antigravity) | High | High | Own what platforms won't: model neutrality, outcome pricing, small-team UX, evidence, human support. Integrate with their agents as adapters |
| Reliability on real small-team codebases | High | Medium | Bug and Maintenance lines first; order sizing; test-first orders; holdout scenarios |
| Token-cost volatility or price increases | High | Medium | Routing, caching, batch; bring-your-own-key mode; price review before GA; per-order caps |
| Security incident involving customer code or production | Very high | Low–Medium | Sandbox-only execution; no production credentials; destructive-action gate; SOC 2 Type II; penetration test |
| "Replace engineers" backlash | Medium | Medium | Messaging per §2.3; publish honest failure rates |
| Crowded category; high CAC | Medium | High | Build in public; open line format and benchmark; agency partnerships; Show HN |
| Upstream Paperclip churn | Medium | Medium | Thin fork, upstream contributions, clear module boundaries |
| Copyright of purely AI-generated code; customer compliance (EU Cyber Resilience Act reporting from 11 Sep 2026, full application 11 Dec 2027) | Medium | Medium | Record human-approved specs and edits; SBOM and vulnerability-handling features ([Copyright Office](https://newsroom.loc.gov/news/copyright-office-releases-part-2-of-artificial-intelligence-report/s/f3959c36-d616-498d-b8f9-67641fd18bab), [CRA](https://digital-strategy.ec.europa.eu/en/policies/cra-reporting)) |
| Provider terms for local or bring-your-own-key modes (using personal subscriptions in our product) | Medium | Medium | API keys only in cloud mode; local-runner mode documented per provider terms; legal review before beta |

---

## 8. Recommended Next Steps

### Phase 0: Validate (October to mid-November 2026, 4–6 weeks)
- [ ] **12 design partners:** 5 solo technical founders, 4 small teams, 3 agencies. Real repositories, connected read-only first.
- [ ] **Concierge factory** on the Paperclip fork plus Claude Code and Codex adapters. Run lines L2 (bugs) and L3 (maintenance) first, then L1 (features).
- [ ] **Measure:**
  - first-pass merge rate;
  - false-green rate;
  - change-failure rate;
  - cost per merged change;
  - review time per change;
  - hours saved.
- [ ] **Price test:**
  - Van Westendorp survey plus a paid pilot at Small $3 / Medium $12;
  - measure the share who choose bring-your-own key.
- [ ] **Brand:** 3 finalist names, a USPTO and EUIPO knock-out search, and domains (§2.2).
- [ ] **Go / no-go gates:**
  - first-pass merge rate ≥ 50%;
  - zero false-green;
  - Medium cost ≤ $6 at p50;
  - ≥ 40% of partners "very disappointed" if it went away;
  - ≥ 6 of 12 willing to pay at the tested price.

### Phase 1: Public beta (W0 = week of 25 Jan 2027)
- [ ] Lines **L2 Bug** and **L3 Maintenance** generally available in beta, with **L1 Feature** in preview.
- [ ] Repo X-ray, evidence inbox, outcome pricing, weekly factory report.
- [ ] Solo and Agency plans; founding-member pricing.

### Phase 2: GA (late April 2027)
- [ ] L1 Feature line fully available; **L4 Greenfield SaaS** and **L5 Agency client** lines.
- [ ] Team plan; release and operate integrations; SOC 2 Type I.
- [ ] First "State of AI Software Factories" report, plus the public factory benchmark.

### Phase 3: Expand
- [ ] Mid-market teams (20–100 engineers): SSO, audit exports, SOC 2 Type II.
- [ ] Legacy modernization line as the enterprise wedge.
- [ ] An "OPC operations" layer: the parked front office, revenue and content features, offered for founders' own businesses.

---

## Data Sources

**Primary data**
- US Census Bureau:
  - [SUSB 2021 detailed sizes](https://www2.census.gov/programs-surveys/susb/datasets/2021/) (NAICS 5415, 541511, 541512, 511210);
  - [Nonemployer Statistics 2023](https://www2.census.gov/programs-surveys/nonemployer-statistics/datasets/2023/historical-datasets/) (NAICS 5415).
- [METR time horizons](https://metr.org/time-horizons/), raw file `benchmark_results_1_1.yaml` (pulled 2026-10-04).
- Google Trends via pytrends, 2025-01-01 to 2026-10-03.
- RDAP: Verisign (`.com`) and Google Registry (`.dev`), 2026-10-04.
- Trustpilot business pages (rendered 2026-10-04): [Lovable](https://www.trustpilot.com/review/lovable.dev), [Replit](https://www.trustpilot.com/review/replit.com), [Base44](https://www.trustpilot.com/review/base44.com), [Emergent](https://www.trustpilot.com/review/emergent.sh), [Bolt.new](https://www.trustpilot.com/review/bolt.new), [Cursor](https://www.trustpilot.com/review/cursor.com), [Windsurf](https://www.trustpilot.com/review/windsurf.com).
- Hacker News comments via the [Algolia HN Search API](https://hn.algolia.com/api), July–October 2026.
- [Claude API pricing](https://platform.claude.com/docs/en/about-claude/pricing); [Claude Code cost guidance](https://code.claude.com/docs/en/costs).
- Paperclip repository: `packages/adapters/`, `packages/plugins/sandbox-providers/`, `packages/db/src/schema/`, `server/src/services/`, `doc/`.

**Research and industry**
- [JetBrains AI coding agent adoption 2026](https://blog.jetbrains.com/research/2026/08/ai-coding-agent-adoption-2026/)
- [Stack Overflow 2025 survey press release](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/)
- [Anthropic 2026 Agentic Coding Trends Report](https://resources.anthropic.com/2026-agentic-coding-trends-report)
- [DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/)
- [CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report)
- [Veracode 2026](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/)
- [CSA research note](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/)
- [Indeed Hiring Lab](https://hiringlab.indeed.com/2026/07/08/ai-and-job-postings-from-destruction-to-creation/)
- [BLS](https://www.bls.gov/ooh/computer-and-information-technology/software-developers.htm)
- [SlashData](https://www.slashdata.co/post/global-developer-population-trends-2025-how-many-developers-are-there)
- [Stripe solo founders](https://stripe.com/blog/top-solo-founder-traits); [HSEP on Carta](https://hsep.substack.com/p/solo-founders)
- [Simon Willison: five levels](https://simonwillison.net/2026/Jan/28/the-five-levels/); [Simon Willison: StrongDM](https://simonwillison.net/2026/Feb/7/software-factory/)
- [Northflank sandbox pricing](https://northflank.com/blog/ai-sandbox-pricing)

**Competitors and news**
- Cursor: [CNBC](https://www.cnbc.com/2026/06/16/spacex-spcx-cursor-acquisition-ipo.html), [Dealroom](https://dealroom.co/news/134107-cursor-tops-4b-annualized-revenue/), [Gartner MQ post](https://cursor.com/blog/cursor-leads-gartner-mq-2026), [Graphite acquisition](https://devops.com/cursor-acquires-graphite-to-streamline-ai-powered-development/)
- Anthropic and OpenAI: [VentureBeat](https://venturebeat.com/technology/anthropic-says-it-hit-a-30-billion-revenue-run-rate-after-crazy-80x-growth), [VKTR on Code Review](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/), [OpenAI Gartner post](https://openai.com/index/gartner-2026-agentic-coding-leader/)
- GitHub and Microsoft: [Microsoft FY26 Q2](https://www.microsoft.com/en-us/investor/events/fy-2026/earnings-fy-2026-q2), [Agent HQ](https://github.blog/news-insights/company-news/welcome-home-agents/), [usage-based billing](https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/), [The Register](https://www.theregister.com/ai-and-ml/2026/06/02/github-copilot-users-threaten-exit-as-metered-billing-kicks-in/5249826)
- Funding and valuations: [Cognition (Bloomberg)](https://www.bloomberg.com/news/articles/2026-09-08/ai-startup-cognition-raises-2-billion-at-a-48-billion-value), [Factory (DevOps.com)](https://devops.com/factory-raises-200m-as-it-builds-agents-across-the-software-lifecycle/), [8090 (Ry Walker)](https://rywalker.com/research/8090-software-factory), [EY and 8090](https://www.ey.com/en_us/newsroom/2026/03/ernst-young-llp-and-8090-launch-ey-ai-pdlc), [Lovable](https://lovable.dev/blog/series-c), [Replit (Sacra)](https://sacra.com/c/replit/), [Resolve AI (Bloomberg)](https://www.bloomberg.com/news/articles/2026-02-04/resolve-ai-hits-1-billion-valuation-for-outage-thwarting-ai-agents)
- AWS and Google: [AWS frontier agents](https://aws.amazon.com/blogs/machine-learning/aws-launches-frontier-agents-for-security-testing-and-cloud-operations/), [Google Antigravity](https://antigravity.google/)
- Incidents and costs: [PocketOS (Tom's Hardware)](https://www.tomshardware.com/tech-industry/artificial-intelligence/claude-powered-ai-coding-agent-deletes-entire-company-database-in-9-seconds-backups-zapped-after-cursor-tool-powered-by-anthropics-claude-goes-rogue), [Uber (Forbes)](https://www.forbes.com/sites/janakirammsv/2026/05/17/uber-burns-its-2026-ai-budget-in-four-months-on-claude-code/)
- Pricing summaries (secondary): [Claude plans](https://intuitionlabs.ai/articles/claude-pricing-plans-api-costs), [Cursor](https://dev.to/rahulxsingh/cursor-pricing-in-2026-hobby-pro-pro-ultra-teams-and-enterprise-plans-explained-4b89), [Devin](https://www.usecarly.com/blog/devin-pricing/), [Factory](https://continuumcode.ai/guides/factory-ai-pricing/), [Lovable](https://www.eesel.ai/blog/lovable-pricing), [Replit](https://www.lowcode.agency/blog/replit-pricing-explained)

## Data Quality Notes

- **SUSB 2021** is the latest published firm-size file. It counts employer firms, not individuals. **NES 2023** counts nonemployer establishments. The two don't overlap.
- **Review coding** used keyword rules per theme. Themes overlap. Samples were checked by hand, and precision was good for the money, support and bug themes. A detector for "claimed done but wasn't" was too noisy to report. Trustpilot over-represents non-engineers (app builders). Hacker News over-represents experienced engineers. Read the two together.
- **Reddit** blocked automated access (HTTP 403). **GitHub issue search** was out of scope for this session's access. Both are listed for Phase 0 interviews instead.
- **Revenue figures** come from company statements or reputable press. Gartner's market size is reported secondhand.
- **Cost per change** is modeled from list prices and token assumptions, and cross-checked with Anthropic's published enterprise average. Phase 0 must replace it with measured data.
- **Google Trends** values are relative indexes with sampling noise.
- **Domain** results are RDAP registration status, not trademark clearance.
