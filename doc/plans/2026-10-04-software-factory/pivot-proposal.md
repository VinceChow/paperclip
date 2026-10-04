# Pivot Proposal: From the OPC Platform to an AI Software Factory

| | |
|---|---|
| **Date** | 2026-10-04 |
| **Status** | **Approved 2026-10-04.** All nine recommendations in §9 were accepted as written. The rewritten documents are in this folder (see the [README](./README.md)); the OPC set is kept, marked as superseded. |
| **Scope** | Every document in [`2026-09-26-opc-platform/`](../2026-09-26-opc-platform/README.md): market research, industry kits, reliability and cost harness, marketing plan, product feature strategy, X guide and PRD |
| **Method** | New desk research (pulled 2026-10-04) • 656 one- and two-star Trustpilot reviews of seven AI-coding products, coded by theme • 246 four- and five-star reviews • METR time-horizon raw data • Google Trends • Census SUSB 2021 and NES 2023 firm counts • Claude API price list • a capability check of this repository |

---

## 0. The proposal on one page

**What changes.** The product stops being "an AI team for consultants and coaches." It becomes an **AI software factory**: specs go in; planned, built, tested, secured, deployed and maintained software comes out, with evidence for every change.

**My recommendation as CPO: pivot, but pick a sharp target.**
- **Target:** small software companies.
  - Solo technical founders.
  - Product teams of up to 20 engineers.
  - Development agencies and freelancers.
- **Not first:** large enterprises (eight funded vendors already serve them), or non-technical "prompt to app" users (Lovable, Replit and others).
- **Why this target:**
  1. **Demand is real and growing.**
     - 90% of professional developers use AI coding agents every week.
     - Solo founders formed 63% of new C corporations on Stripe Atlas in Q2 2026.
     - AI-native solo startups make about 2x the revenue of other solo startups by year two.
  2. **The bottleneck has moved.** Generating code is no longer the hard part. Verification, safety and cost are:
     - AI-written pull requests have about 1.7x more issues than human-written ones.
     - Security pass rates are stuck at 56%.
     - Developers can fully delegate only 0–20% of their tasks.
     - Token bills have broken budgets: Uber used its 2026 AI budget in four months.
     
     Small teams feel this most, because they have no platform team to build the guardrails.
  3. **The work we already did transfers directly.** Outcome contracts, risk tiers, the decision inbox, "failed jobs are free," the trust ladder, fair billing and the weekly review answer exactly the complaints customers make about AI-coding products. In 656 negative reviews:
     - 66% complain about money: 49% about credits and usage, 42% about billing and refunds;
     - 39% complain about support;
     - only 32% complain about bugs and loops.

**Change the message from "replace engineers" to "engineers run the factory."** Your thesis is that AI changes how software engineers work. The evidence supports that thesis. It does not support "replaces engineers" yet:
- most new hiring growth is for senior roles that direct the work;
- developers still trust AI output less than they did a year ago.

Our first buyers are engineers and technical founders. "Stop typing code. Start running a factory" wins them over; "replace engineers" pushes them away and invites claims we can't prove (§2).

**Reconsider building from scratch.** The PRD assumed a from-scratch build. For a software factory, though, this repository (Paperclip: MIT-licensed, about 47K GitHub stars within weeks of its March 2026 launch, per [Webvise](https://www.webvise.io/blog/paperclip-ai-company-orchestration)) already provides most of the control plane:
- issues and work breakdown;
- 12 coding-agent adapters;
- isolated workspaces;
- managed GitHub identity;
- low-trust presets for untrusted input;
- approvals, budgets, completion contracts and evals.

Rough estimate: about 60–75 person-weeks on Paperclip versus about 145 from scratch (§6).

**Nine decisions for you** are listed in §9. The most important are the target customer (D1), the message (D2), the foundation (D4) and the launch date (D7).

---

## 1. What the evidence says

### 1.1 The concept

| Source | What it says |
|---|---|
| **Dan Shapiro's five levels** (Jan 2026) | **Level 0:** autocomplete. **Level 1:** coding intern. **Level 2:** junior developer, every line reviewed. **Level 3:** AI writes most code and the human becomes a full-time reviewer. **Level 4:** humans write specs and agents do the work. **Level 5:** the "dark software factory," a black box that turns specs into software ([Simon Willison](https://simonwillison.net/2026/Jan/28/the-five-levels/)) |
| **StrongDM's Software Factory** (Feb 2026) | **Rules:** "Code must not be written by humans. Code must not be reviewed by humans." **How they check the work:** holdout scenarios kept outside the codebase, a "satisfaction" score, and clones of Okta, Jira, Slack and Google services (a "Digital Twin Universe"). **Scale:** 3 engineers. **Token target:** at least $1,000 per engineer per day ([Simon Willison](https://simonwillison.net/2026/Feb/7/software-factory/)) |
| **8090 Software Factory** | **Modules:** Requirements, Blueprints, Work Orders, Tests, Feedback. **Price:** $200 per user per month, tokens extra; enterprise from $1M a year. **Funding and customers:** EY deployment (Mar 2026); $135M Series A ([Ry Walker](https://rywalker.com/research/8090-software-factory), [EY](https://www.ey.com/en_us/newsroom/2026/03/ernst-young-llp-and-8090-launch-ey-ai-pdlc)) |
| **Factory ("Droids")** | **Coverage:** agents for review, security, docs, QA and incident response. **Funding:** $200M at $5B (Sep 2026). **Customers:** Nvidia, Adobe, Palo Alto Networks ([DevOps.com](https://devops.com/factory-raises-200m-as-it-builds-agents-across-the-software-lifecycle/)) |
| **AWS "frontier agents"** | **Generally available (31 Mar 2026):** Security Agent and DevOps Agent. **Still in preview:** Kiro autonomous agent ([AWS](https://aws.amazon.com/blogs/machine-learning/aws-launches-frontier-agents-for-security-testing-and-cloud-operations/)) |

**Working definition for us:** a software factory is a governed system in which agents carry work through every stage (spec → plan → build → verify → release → operate). It differs from a coding agent in three ways:
1. every change carries evidence that it meets its definition of done;
2. agents cannot harm production by design;
3. humans step in only where risk calls for it.

### 1.2 Demand and money

| Signal | Number | Source |
|---|---|---|
| Developers using AI coding agents at work, weekly / daily | **90% / 68%** (15,000+ developers, May–Jul 2026) | [JetBrains Research](https://blog.jetbrains.com/research/2026/08/ai-coding-agent-adoption-2026/) |
| Most-used agent | Claude Code is used by 39% and is the main tool for 31%; Copilot 21%; Codex 16%; Cursor 12% | Same |
| Cursor | $4B+ annualized revenue (Jun 2026); acquired by SpaceX for **$60B** (closed 14 Aug 2026) | [CNBC](https://www.cnbc.com/2026/06/16/spacex-spcx-cursor-acquisition-ipo.html), [Dealroom](https://dealroom.co/news/134107-cursor-tops-4b-annualized-revenue/) |
| Claude Code | Run-rate revenue above **$2.5B** (12 Feb 2026) | [VentureBeat](https://venturebeat.com/technology/anthropic-says-it-hit-a-30-billion-revenue-run-rate-after-crazy-80x-growth) |
| Cognition (Devin + Windsurf) | Run-rate about **$900M**; $2B raised at **$48B** (Sep 2026) | [Bloomberg](https://www.bloomberg.com/news/articles/2026-09-08/ai-startup-cognition-raises-2-billion-at-a-48-billion-value) |
| Lovable / Replit | $13.3B valuation (Aug 2026) / $9B valuation with about $525M ARR | [Lovable](https://lovable.dev/blog/series-c), [Sacra](https://sacra.com/c/replit/) |
| GitHub Copilot | **4.7M** paid subscribers, up 75% year over year (Jan 2026) | [Microsoft FY26 Q2](https://www.microsoft.com/en-us/investor/events/fy-2026/earnings-fy-2026-q2) |
| Gartner category | The first "Enterprise AI Coding Agents" Magic Quadrant (20 May 2026). Leaders: Anthropic, Cursor, GitHub, OpenAI. Market reported at about **$10B** in 2026 | [Cursor](https://cursor.com/blog/cursor-leads-gartner-mq-2026), [Enterprise DNA (secondary)](https://enterprisedna.co/resources/news/gartner-enterprise-ai-coding-agents-10-billion-market-2026/) |
| Solo founders | **36%** of startups on Carta in 2025. **63%** of Stripe Atlas C corporations in Q2 2026 (all-time high). By year two, AI-native solo startups make about 2x the revenue of other solo startups | [Carta via HSEP](https://hsep.substack.com/p/solo-founders), [Stripe](https://stripe.com/blog/top-solo-founder-traits) |
| AI SRE and review | Resolve AI valued at $1B+ (Feb 2026). Cursor bought Graphite (Dec 2025). Anthropic launched Code Review (Mar 2026; about $15–25 per review) | [Bloomberg](https://www.bloomberg.com/news/articles/2026-02-04/resolve-ai-hits-1-billion-valuation-for-outage-thwarting-ai-agents), [DevOps.com](https://devops.com/cursor-acquires-graphite-to-streamline-ai-powered-development/), [VKTR](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/) |

**What this means:** demand is proven and enormous, and so is the competition. A new entrant can't win "best coding agent." Labs and platforms ship that layer at model cost. The open ground is the **factory system around the agents** for a buyer the leaders don't focus on.

### 1.3 Capability trend (METR raw data, pulled 2026-10-04)

| Model (release) | 50% time horizon | 80% time horizon |
|---|---|---|
| GPT-5 (Aug 2025) | 3.4 h | 38 min |
| Claude Opus 4.5 (Nov 2025) | 4.9 h | 49 min |
| Claude Opus 4.6 (Feb 2026) | 12.0 h | 70 min |
| Claude Mythos Preview, early (Apr 2026) | **17.4 h** | **3.1 h** |

A **50% time horizon** is the length of task, measured in expert-human time, that an agent finishes half the time. METR's fitted doubling time since 2023 is **about 129 days** (95% CI 104–158) ([METR](https://metr.org/time-horizons/)).

**Design implication:** right now, the length of task an agent finishes reliably (80%) is about 3 hours of human work. So the factory must split work into orders that agents can finish reliably, and verify each order. If the trend holds, that size grows about 7x a year. The planner should therefore grow order size automatically as measured pass rates rise. That is how a factory moves from Level 4 toward Level 5 safely.

### 1.4 The bottleneck has moved to verification, safety and cost

| Finding | Source |
|---|---|
| AI raises delivery throughput **and** instability (more change failures and rework); AI amplifies what an organization already has | [DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/) |
| AI-authored pull requests had about **1.7x** more issues (10.83 vs 6.45 per PR; security issues up to 2.74x) | [CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report) |
| Security pass rate of AI-generated code is flat at **56%** across 100+ models | [Veracode 2026](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/) |
| Developers use AI in about 60% of their work but can **fully delegate only 0–20%** of tasks | [Anthropic 2026 Agentic Coding Trends Report](https://resources.anthropic.com/2026-agentic-coding-trends-report) |
| Trust in AI accuracy fell to 29%; 46% actively distrust it; the top complaint, at 66%, is code that is "almost right" (Stack Overflow 2025 survey) | [Stack Overflow survey (via ADTmag)](https://adtmag.com/blogs/watersworks/2026/01/stack-overflow-survey.aspx) |
| Code output per Anthropic engineer rose about 200% in a year, and review became the bottleneck | [VKTR](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/) |
| An agent deleted a production database **and its backups** in 9 seconds (PocketOS, Apr 2026). The real failure was an over-privileged token plus no gate on destructive actions | [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/claude-powered-ai-coding-agent-deletes-entire-company-database-in-9-seconds-backups-zapped-after-cursor-tool-powered-by-anthropics-claude-goes-rogue) |
| About 5,000 apps built with vibe-coding tools were leaking sensitive data (RedAccess, May 2026); 2,038 critical vulnerabilities across 1,400 apps (Escape) | [CSA research note](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/) |
| Enterprise Claude Code cost averages **$150–250 per developer per month**. Uber used its 2026 AI budget in four months, at $500–2,000 per engineer per month | [Claude Code docs](https://code.claude.com/docs/en/costs), [Forbes](https://www.forbes.com/sites/janakirammsv/2026/05/17/uber-burns-its-2026-ai-budget-in-four-months-on-claude-code/) |
| GitHub Copilot's switch to usage-based billing (1 Jun 2026) caused a backlash. Developers reported using 8% of a monthly allowance in two hours, and quotas that would run out in under two days | [The Register](https://www.theregister.com/ai-and-ml/2026/06/02/github-copilot-users-threaten-exit-as-metered-billing-kicks-in/5249826) |

### 1.5 Voice of customer: 656 negative reviews of AI-coding products

**Sample:** unique one- and two-star Trustpilot reviews, August 2025 to October 2026 (median June 2026), coded by keyword theme and spot-checked by hand.

| Product | Trustpilot score (reviews) |
|---|---|
| Lovable | 4.2 (1,758) |
| Replit | 2.8 (1,555) |
| Base44 | 2.8 (898) |
| Emergent | 2.8 (636) |
| Bolt.new | 1.6 (203) |
| Cursor | 1.5 (337) |
| Windsurf | 1.4 (59) |

Devin and Factory have too few Trustpilot reviews to code.

| Complaint theme | Share of negative reviews | Highest |
|---|---|---|
| **Any money issue** (credits, usage, billing, refunds) | **65.7%** | — |
| Credits and usage burn | 48.6% | Emergent 60%, Windsurf 55% |
| Billing, refunds, cancellation | 41.6% | Cursor 67%, Replit 54% |
| Support unresponsive or unhelpful | 39.3% | Emergent 53%, Cursor 50% |
| Bugs, loops, "fixes one thing, breaks another" | 31.9% | Emergent 42%, Replit 40% |
| **Paid for failure** (credits burned on errors or loops) | **24.4%** | — |
| "Scam" or "misleading" language | 17.5% | Emergent 27%, Replit 24% |
| Quality got worse | 11.9% | Cursor 22% |
| Deployment and production problems | 9.9% | Emergent 19% |
| Destructive changes or lost work | 8.1% | Base44 12%, Cursor 11% |

**Positive reviews (246):**
- 31% praise support;
- 23% mention speed;
- 18% mention ease;
- 15% mention launching a real business or app.

**The pattern matches our earlier OPC research almost exactly** (billing 53%, support 40%, credits 37%). Customers forgive weak AI faster than unfair money and silence. "Failed work is free," a predictable price and humans who answer are still the cheapest differentiators to own.

### 1.6 Search interest (Google Trends, worldwide, quarterly average, 0–100 within the set)

| Term | Q1 2025 | Q3 2025 | Q1 2026 | Q2 2026 | Q3 2026 |
|---|---|---|---|---|---|
| software factory | 4.8 | 14.1 | 22.6 | 31.2 | 20.7 |
| AI software factory | 0.0 | 2.2 | 3.8 | 6.1 | 3.4 |
| dark factory | 3.1 | 6.5 | 12.5 | 18.4 | 8.3 |
| vibe coding | 11.5 | 43.9 | 65.1 | 68.1 | 49.5 |
| AI coding agent | 0.9 | 6.2 | 21.2 | 72.4 | 30.7 |

In a second pull, "Claude Code" ran about 13–18x "vibe coding." So "software factory" is a **rising but small** search term: about 4x since Q1 2025, but only about 3% of "Claude Code."

The term is also ambiguous. It is used by US defense "software factories" and by manufacturing software. Every term dipped in Q3 2026, as it did in our September pull, so treat that quarter as noise.

**Conclusion:** use "AI software factory" as the **category** for content, PR and SEO. Brand on outcomes, not on the term. The "Factory" brand belongs to Factory.ai, and "Software Factory" is 8090's product name.

### 1.7 Jobs: how engineers work is changing; they are not being replaced yet

- US software-development postings on Indeed are up almost 15% since Claude Code launched (February 2025), but remain 27.5% below their pre-pandemic level.
- **71%** of the increase from May 2025 to May 2026 came from senior roles; 37% came from jobs with "AI" in the title ([Indeed Hiring Lab](https://hiringlab.indeed.com/2026/07/08/ai-and-job-postings-from-destruction-to-creation/)).
- METR's 2025 trial found experienced developers were 19% *slower* with AI. Its 2026 follow-up points to an 18% speed-up, but METR calls that data unreliable ([METR summary](https://ingenire.com/blog/metr-2026-developer-productivity-study)).

---

## 2. Is the "software factory replaces how engineers work" thesis right?

**Where the evidence supports you:**
- Capability is compounding (§1.3).
- Agents are already near-universal (§1.2).
- A three-person team has shipped security software without writing or reviewing code (§1.1).
- Hiring has already shifted toward senior engineers who direct the work (§1.7).

The way software gets made is moving from writing code to **specifying, verifying and operating**. That is a factory.

**Where it doesn't support you yet:**
- Full delegation is still 0–20% of tasks.
- Trust is falling.
- AI-authored changes carry more defects and security flaws.
- Teams without strong testing and CI see more instability, not less.

A "lights-out" factory on a typical small team's codebase would fail today.

**What this means for the product:**
1. **Ship Level 4 by default, and earn Level 5 one factory line at a time.** Humans approve specs and risky changes; agents do the rest. A line runs lights-out only after its measured track record earns it (the trust ladder from the OPC work).
2. **Verification is the product.** Every change ships with evidence: tests, holdout scenarios, security scans, a preview environment and the review record.
3. **Safe by construction.**
   - Agents work only in sandboxes and never hold production credentials.
   - Destructive and irreversible actions always need a human.
   - This is the PocketOS lesson.
4. **Fix the economics.**
   - The price is known before work starts.
   - Failed work is free.
   - Hard caps.
   - Optional bring-your-own model key.

**Messaging recommendation (D2):**
- **Use:** "Engineers stop typing code and start running factories" and "Run a whole software company with a team of one."
- **Avoid:** "replace engineers" on the landing page, in ads or at launch.

Why:
- our champions are engineers;
- the FTC rules from our earlier compliance work also apply to productivity claims;
- the hiring data doesn't back it yet.

You can still say it in your own build-in-public voice as a belief ("I think this is how all software gets made by 2030"), rather than as a product claim.

---

## 3. Where to play

| Option | Who | Competition | Fit with our assets | Speed to revenue | Build-in-public fit | Verdict |
|---|---|---|---|---|---|---|
| **A. Enterprise engineering orgs** | 100+ engineers | Extreme: GitHub, Cursor, Anthropic, OpenAI, Cognition, Factory, 8090, AWS, Google | Medium: needs SSO, on-premises deployment, FedRAMP and field sales | Slow (6–12-month cycles) | Weak | **Later**, once we have evidence and SOC 2 Type II |
| **B. Non-technical founders** ("prompt to app") | OPC owners, domain experts | Extreme: Lovable, Replit, Bolt, Base44, Emergent | High on simplicity and fairness, low on code depth | Fast, but high churn | Strong | **Not first.** Our VOC data shows this segment's pain is exactly what it punishes |
| **C. Small software companies** (solo technical founders, teams of 1–20 engineers, agencies and freelancers) | People who ship and maintain real products or client work | High, but no leader is built for them as a governed end-to-end factory | **Highest:** contracts, risk tiers, trust ladder, fair billing, Paperclip control plane, build-in-public | Medium-fast (self-serve plus founder-led sales to agencies) | **Strongest:** developers and indie founders live on X | **Recommended** |
| **D. Open-source control plane, paid cloud** | Developers who self-host | Medium: Agent HQ, orchestrator start-ups | High if built on Paperclip | Slow to monetize | Strong | **As a channel, not the business:** open-source the line format and benchmark (§4.5) |

**Sizing for option C (order of magnitude; assumptions stated):**

| Item | Number | Source or assumption |
|---|---|---|
| US IT and software nonemployer businesses earning ≥ $50K | 95,641 (of 343,329) | Census NES 2023, NAICS 5415 (from our OPC research) |
| US computer-systems-design employer firms with under 20 employees | 113,874 | Census SUSB 2021, NAICS 5415 |
| US software publishers with under 20 employees | 10,231 | Census SUSB 2021, NAICS 511210 |
| **US core accounts** | **≈ 220K** | Conservative. Undercounts SaaS founders filed under other industry codes |
| Revenue per account | $200–1,000 per month | Assumption: platform fee plus about 20–80 verified changes a month (§4.6) |
| **US core serviceable market** | **≈ $0.5–2.6B a year** | 220K × $2.4–12K |
| Global core | ≈ $2–10B a year | Assumes the US is about 20–25% of spend. Validate |
| 3-year obtainable share | $20–40M ARR | 1–2% of US core accounts at about $400 a month, plus a similar amount internationally |
| Context | US software and QA payroll ≈ **$255B** a year (1.9M jobs × $134K median); enterprise AI coding agents ≈ $10B (2026) | [BLS](https://www.bls.gov/ooh/computer-and-information-technology/software-developers.htm); Gartner, reported |

**Compared with the OPC plan:** the obtainable share is similar or smaller in year 3, because the field is more crowded. But revenue per account is 3–15x higher, and the path up-market (option A) is open. If factories really do take over engineering labor, revenue per account is the number that grows. I'd still rather be honest: this pivot is a bigger, riskier bet, not a safer one.

---

## 4. The product concept (to be detailed in the rewritten docs)

### 4.1 Positioning (draft)

For solo founders, small software teams and development agencies who need to ship more than their headcount allows, **[Brand] is the AI software factory**: it turns specs into verified, deployed and maintained software.

Unlike coding agents that hand you code to check, [Brand]:
- proves every change against its definition of done;
- keeps agents away from production by design;
- charges only for work that passes.

**Tagline candidates:**
- "Specs in. Shipped software out."
- "Run a software company of one."
- "Stop typing. Start running the factory."

### 4.2 The factory line

```
 Intake ─► Spec ─► Plan ─► Build ─► Verify ─► Review ─► Release ─► Operate ─► Learn
   │        │        │        │         │          │          │          │         │
 issue,   owner   orders   agents in  tests,     evidence-  preview,   monitor,  weekly
 bug,     approves sized    sandboxes, scenarios, first      flags,     triage,   factory
 Sentry,  (High)  to what   any model  security,  inbox;     staged     auto-fix  report,
 voice    spec    agents    (adapters) twin       risk tier  deploy,    PRs       evals
 note     diff    finish               services   decides    rollback             from edits
                  reliably
```

| Station | Default autonomy at launch | "Done" means |
|---|---|---|
| Spec | Human approves the spec for new features; small fixes generate their own spec | Acceptance criteria written as checks |
| Plan | Automatic | Orders sized to the repository's measured success rate; dependencies set |
| Build | Automatic in an isolated sandbox | Code compiles; the order's checks are written before the code |
| Verify | Automatic | Unit, integration and holdout scenarios pass; SAST, dependency and secret scans are clean; preview environment is up |
| Review | **Risk tier decides.** Low: auto-merge after a 20-run track record. Medium: batch approval. High: individual approval | Evidence card with a ✓ or ✗ per criterion |
| Release | Behind feature flags; staged rollout; automatic rollback | Health checks pass after deploy |
| Operate | Incidents opened and diagnosed automatically; fixes come back as new orders | Fix verified in a preview environment, then released |
| Learn | Automatic | Edits and rejections become eval cases |

**Change risk tiers** (adapted from the OPC risk tiers):

| Tier | Types of change | Default handling |
|---|---|---|
| **Low** | Docs, tests, refactors fully covered by tests, dependency patch versions, lint fixes | Automatic once trusted |
| **Medium** | Features behind flags, minor dependency upgrades, UI changes | Batch approval |
| **High** | Schema migrations, auth, payments, permissions, infrastructure, deleting data, anything touching production secrets | Individual approval always. Never automatic in v1 |

### 4.3 What carries over from the OPC work

| OPC concept | Software factory version |
|---|---|
| Outcome contract | **Executable definition of done:** acceptance checks, holdout scenarios, scans, preview health |
| "Failed jobs are free" | **Failed orders are free;** you pay only for merged, verified changes |
| Risk tiers, decision inbox, batch approval, undo | Change risk tiers; **evidence-first review inbox**; batch approval; rollback |
| Trust ladder | **Lights-out, earned per factory line** from measured track records |
| Business Brain | **Product Brain:** architecture map, conventions, decisions, domain glossary, customer feedback |
| Business X-ray (zero-prompt start) | **Repo X-ray:** test gaps, vulnerable dependencies, flaky tests, missing CI and open bugs become the first five suggested orders. Nothing changes until approved |
| Friday Review | **Weekly factory report:** what shipped, cycle time, change-failure rate, cost per change, **what failed and why** |
| Industry kits | **Factory lines** (blueprints per kind of work and stack), §4.5 |
| Safe-action rules | No production credentials for agents; sandbox-only execution; gates on destructive actions; mock "twin" services |
| Fair billing and human support | Unchanged, and even more valuable here (§1.5) |
| Build in public | Stronger fit: **"the factory builds the factory,"** with public weekly metrics |

**Parked (dropped from the core, kept as notes):** front office and speed-to-lead, revenue loop, content engine, client list, the property-agent kit and receptionist, WhatsApp/SMS, and the Gmail restricted-scope work. That last item removes the Google security-assessment risk entirely.

### 4.4 Seven bets (replacing B1–B7)

| # | Bet | Target to prove (not a public claim) |
|---|---|---|
| F1 | **Zero-prompt start:** Repo X-ray plus Product Brain | Connect a repo → first merged, verified change in **≤ 30 min** |
| F2 | **Verified changes:** executable definition of done; holdout scenarios; twin services | First-pass merge rate ≥ 60% (beta) / ≥ 75% (GA); **zero "false green"** (merged and marked verified, but failing within 7 days) |
| F3 | **Safe by construction:** sandboxes, least privilege, destructive-action gates | Zero production-credential exposure; 100% of High-tier changes approved by a human |
| F4 | **Decisions, not code reviews:** evidence-first inbox, batch approval, trust ladder | Median review decision ≤ 60 s per Medium change |
| F5 | **Predictable economics:** priced before work, failed work free, caps, bring-your-own key | Zero surprise charges; cost per change shown on every card |
| F6 | **Operate what you ship:** release, monitor, auto-fix loop | Change-failure rate ≤ 15%; mean time to restore ≤ 1 h for our releases |
| F7 | **The weekly factory report** | ≥ 60% weekly open rate; honest failure section in every report |

### 4.5 Factory lines (replacing the industry kits)

| Line | What it does | Why first |
|---|---|---|
| **L1 Feature line** (existing TypeScript/Python web app) | Spec → orders → verified PRs → preview | The core job |
| **L2 Bug line** | Issue or error-tracker event → failing test that reproduces it → fix → verify | Easiest to verify; fastest trust |
| **L3 Maintenance line** | Dependency upgrades, security patches, flaky tests, coverage | Low risk; first lights-out candidate |
| **L4 Greenfield SaaS line** | Spec → new app on a standard blueprint (Next.js, Postgres, auth, Stripe) → deployed | For solo founders; competes with Lovable on production quality |
| **L5 Agency client line** | Separate client workspaces; handover docs; per-client cost reports | Agencies pay for throughput |
| Later | API and integrations; mobile (Expo); data pipelines; **legacy modernization** (the enterprise wedge) | — |

We open-source the **line format** and a **public factory benchmark** (real-world tasks with holdout scenarios and the cost per verified change). This is the category-creation and PR asset, and the community flywheel that replaces the kit marketplace.

### 4.6 Economics (hypotheses to validate)

**Cost per verified change,** modeled on current list prices: Sonnet 5.5 at $2/$10 per million tokens; Opus 5.5 at $4/$20; cache reads $0.20.

| Size | Model mix | Modeled cost |
|---|---|---|
| Small (≤ 30 min of human work) | Sonnet build, light review | $1–2 |
| **Medium (1–3 h)** | Opus plan (about $0.60) + Sonnet build (about $2.50) + review agents (about $0.90) + sandbox/CI (about $0.15) + a 30% revision allowance (about $0.75) | **≈ $5** |
| Large (> 3 h) | Split by the planner into Medium orders | $10–25 if not split |

Cross-check: Anthropic's enterprise average of about $13 per active developer-day, at 2–4 changes a day, is about $3–6 per change. A human doing a Medium change at the BLS median wage plus overhead costs about $250–340.

**Pricing (D5): two models to test in Phase 0.**
- **(a) Outcome pricing (default):**
  - a small platform fee per workspace;
  - **a fixed price per merged change**, quoted before work starts (for example Small $3, Medium $12);
  - failed or abandoned orders cost nothing;
  - a hard monthly cap you set.
  
  At about $5 of cost plus about $1 of failure overhead, a Medium change has a gross margin of about 50%.
- **(b) Bring your own key:**
  - platform fee per seat or workspace;
  - you pay your model provider directly at zero markup;
  - per-order budget caps still apply.
  
  For power users and agencies.

**What we drop from the OPC pricing:** $29/$79/$199 plans with deliverable allowances. Software-factory costs are about 10x higher per unit, so those plans don't work here.

---

## 5. Document-by-document change list

The size of each change is the share of content that would be new.

### 5.1 `market-research.md`: rewrite (about 80% new)

| Keep | Change | Drop | New |
|---|---|---|---|
| Method, data-quality notes, sources format, scorecard format, Trends method | Executive summary; market overview; sizing (§3 here); positioning (category = "AI software factory"; naming conflicts with Factory.ai and 8090; "OPC" becomes an audience phrase, not a category); target market and personas; competitive landscape; feasibility; pricing; risks; next steps | Consultant/coach/creator/property personas; the OPC trademark section (moved to an appendix) | Capability-trend section (METR); verification-bottleneck evidence (§1.4); VOC summary (§1.5); jobs data (§1.7); segment-map table (who serves whom, pricing model, what they leave open) |

**New personas:**

| Persona | Snapshot | What they need |
|---|---|---|
| **Sam**, solo technical founder | 1 SaaS, $8K MRR, maintains alone | Ship features while sleeping; no 2 a.m. incidents |
| **Ines**, agency owner | 6 people, 12 client repos | Throughput and margin per client; handovers |
| **Raj**, CTO | 8-person startup | Ship more without hiring; keep quality and security |
| **Dana**, freelance developer | Billing by project | Finish fixed-price work faster at a provable quality |

### 5.2 `industry-kits.md` → `factory-lines.md`: rewrite (about 85% new)

| Keep | Change | Drop | New |
|---|---|---|---|
| Verdict structure (horizontal product, packaged lines); anatomy pattern (team, workflows, contracts, guardrails, evals); marketplace idea; Phase 0 validation | Scoring criteria become demand × ease of verification × risk × cost × differentiation | All five industry kits | Lines L1–L5 in detail; line spec in YAML; open-source line format; public benchmark |

### 5.3 `reliability-cost-harness.md`: major revision (about 50% new)

| Keep | Change | Drop | New |
|---|---|---|---|
| Design principles; the outcome loop; contract schema (extended); retry and escalation policy; budget layers; cost levers (caching, routing, batch) | **Failure evidence** for coding (§1.4); **verification tiers** for code (static checks → tests → holdout scenarios → twin services → security scans → preview → canary); **metrics** add the DORA four, first-pass merge rate, revert rate and escaped defects; **prices** updated; per-user cost model becomes **cost per change and per account** (§4.6); the "Paperclip exists vs gap" table redone for the factory | OPC job types (lead reply, invoices, posts) | Sandbox and twin-service design; order sizing from the METR horizon; destructive-action gate; StrongDM-style holdout scenarios |

### 5.4 `marketing-plan.md`: major revision (about 60% new)

| Keep | Change | Drop | New |
|---|---|---|---|
| Structure (strategy on one page, KPIs, messaging house, landing-page architecture, waitlist, experiments, compliance checklist, launch-week format, gated paid, lifecycle, measurement, budget, 90-day calendar) | **Audience and channels:** X, Hacker News (Show HN), GitHub, Reddit (r/SaaS, r/ExperiencedDevs, r/webdev), developer YouTube, newsletters and podcasts, Discord. **Big idea:** "Company of One, Run in Public" becomes "**The factory builds the factory**," with public weekly factory metrics. **Community:** OPC Club becomes a builders' community of founders and agencies. **Creators** become developer creators and agency partners. **Unit economics:** higher revenue per account, new CAC limits. **Trial:** connect repo → X-ray → first merged change. **Language rules** add no unproven productivity or "replace engineers" claims | Industry kit pages (`/for/consultants` …) | `/for/founders`, `/for/agencies`, `/for/teams` plus pages per line; the open benchmark and an annual "State of AI Software Factories" report as the PR engine; launch on Hacker News plus Product Hunt; comparison pages written fairly |

### 5.5 `product-feature-strategy.md`: rewrite (about 75% new)

| Keep | Change | Drop | New |
|---|---|---|---|
| Method (VOC coding, principles, bets, 10–100x scorecard, RICE, roadmap, anti-features, validation plan) | VOC: §1.5, extended with GitHub issues, Hacker News and Reddit. "Where owners leak time and money" becomes **where engineering time leaks** (review queue, CI, incidents, upgrades). Competitor baseline. **Bets F1–F7.** Information architecture: Today / Orders / Releases / Quality / Cost & Report. Backlog re-scored. Paperclip reuse map redone | Front office, revenue loop, content engine, Friday-for-owners copy | Autonomy-level roadmap (Level 3 → 4 → 5 per line); "lights-out" criteria; anti-features (no "replace engineers" autopilot; no production credentials for agents; no opaque credits) |

### 5.6 `x-build-in-public-guide.md`: moderate revision (about 30% new)

| Keep | Change | Drop | New |
|---|---|---|---|
| Parts 1–3 (X basics, setup, lists), 6 (replies), 8 (metrics), 9 (daily routine), 12 (rules); Premium advice | Part 4 (your story: "I'm building a software factory, and it's building itself"); Part 5 pillars ("OPC Data" becomes Factory Data and AI-dev research; the Friday Report shows merged changes, cost per change and failures); accounts to follow (AI engineering, indie hackers, agency owners); the 120-day plan; about 20 of the 30 posts | OPC statistics posts | Security etiquette (never post customer code or secrets; responsible disclosure); live "factory floor" demos; benchmark threads |

### 5.7 `prd.md`: rewrite to v2 (about 70% new)

| Keep | Change | Drop | New |
|---|---|---|---|
| Structure and requirement-ID style; principles format; NFRs (performance, availability, security, accessibility); billing, support, data-and-privacy and internal-tools modules (adapted); risk-tier and decision module (adapted); outcome-contract module (adapted) | **Goals:** time to first merged change; first-pass merge rate; false-green = 0; change-failure rate; cost per change; week-4 retention. **Modules:** ONB → REPO (connect + X-ray); BRN → PRODUCT BRAIN; JOB → ORDERS and PLANNER; OUT → VERIFY; DEC → REVIEW & TRUST; RPT → FACTORY REPORT; CHN (web, PWA, Slack, email); INT (GitHub/GitLab, Linear/Jira, Slack, Vercel/Fly/AWS, Sentry/Datadog). **Architecture** adds a sandbox fleet, runners, version-control integration, an artifact store, twin services and an eval harness. **Compliance:** SOC 2 Type II earlier (customers hand us source code); secrets handling; open-source license scanning; EU Cyber Resilience Act support for customers (vulnerability reporting from 11 Sep 2026; full application 11 Dec 2027); a copyright note (purely AI-generated code may lack copyright protection under the US Copyright Office's 2025 guidance). **Pricing** per §4.6. **Delivery** re-estimated per D4 | LEAD, REV, CNT, CLI modules; Gmail restricted-scope and CASA work; WhatsApp/SMS and 10DLC | BUILD (runners), RELEASE and OPERATE modules; line spec in the appendix; "lights-out" release gates |

### 5.8 Folder and index

**Recommended (D8):** create `doc/plans/2026-10-04-software-factory/` with the rewritten documents. The OPC folder stays as it is, with a "Superseded by …" banner on each file. This keeps the research history and follows the repo's rule of adding to strategy docs rather than replacing them wholesale.

---

## 6. Foundation: from scratch or on Paperclip (D4)

The PRD assumed a from-scratch build. For a software factory, Paperclip's existing capabilities line up closely:

| Factory need | Already in this repository |
|---|---|
| Work orders, breakdown, dependencies | Issues, sub-issues and blocker relationships ([`doc/execution-semantics.md`](../../execution-semantics.md)) |
| Many coding agents, model-neutral | 12 adapters, including Claude Code, Codex, Cursor, Gemini and OpenCode (`packages/adapters/`) |
| Isolated execution | Execution and project workspaces, runtime leases, Daytona-backed runs in evals |
| Safe GitHub access | Managed, token-free `git`/`gh` launchers bound to the run's accepted identity ([`doc/execution-github-identity.md`](../../execution-github-identity.md)) |
| Hostile input (untrusted PRs, tickets) | `low_trust_review` preset ([`doc/LOW-TRUST-PRESETS.md`](../../LOW-TRUST-PRESETS.md)); containerized untrusted-PR review |
| Approvals, budgets, audit | Approvals, budget policies and incidents, activity log |
| Definition of done | `completion_contracts`, `work_assessments` |
| Recurring lines (maintenance, upgrades) | Routines; task watchdog |
| Evals | Runner evals and product end-to-end evals ([`doc/evals.md`](../../evals.md)) |

**Rough effort for the factory P0** (to be re-estimated in the PRD v2):
- **From scratch:** about 145 person-weeks.
- **On Paperclip:** about 60–75 person-weeks. The remaining work is the Repo X-ray, the verification line, the evidence inbox, release and operate integrations, billing, and a simplified factory UI that hides "agent company" concepts.

**Considerations:**
- MIT allows commercial use and forking.
- The "Paperclip" name and brand are not ours.
- Upstream moves fast, which helps (features) and costs (merge work).
- The community (about 47K stars) is a distribution asset if we contribute back.

**Recommendation:** build the factory on a Paperclip fork for the control plane, and own the verification line, the factory UX and the economics layer. If you prefer to stay from scratch, the PRD v2 will keep that assumption, and launch week should move (D7).

---

## 7. Risks of the pivot, and how we'd know we're wrong

| Risk | Impact | Early warning / kill criterion | Mitigation |
|---|---|---|---|
| Labs and platforms bundle "factory" features at model cost | High | Design partners say "Claude Code / Codex / Agent HQ already does this" | Own what platforms won't: model neutrality, outcome pricing, small-team UX, verification evidence, human support |
| Reliability on real small-team codebases is below target | High | First-pass merge rate < 40% after 4 weeks of pilots | Lines L2/L3 first (easiest to verify); order sizing; test-first orders |
| Token costs make outcome pricing unprofitable | High | Cost per Medium change > $8 at p50 | Routing, caching, planner splits; bring-your-own-key plan; price adjustment before GA |
| A security incident involving customer code or production | Very high | Any production-credential exposure | Sandbox-only execution; no production secrets for agents; destructive-action gate; SOC 2 Type II; third-party penetration test |
| "Replace engineers" backlash | Medium | Negative Hacker News or X reaction at launch | Messaging per D2; publish honest failure rates |
| Crowded category; customer acquisition too expensive | Medium | Paid CAC > 12 months of gross margin | Build in public; open benchmark; agency partnerships |
| Building on a fast-moving open-source upstream | Medium | Merge conflicts take more than 20% of engineering time | Thin fork; contribute upstream; clear module boundaries |
| Copyright of purely AI-generated code; customer compliance (EU Cyber Resilience Act) | Medium | Customer legal questions block deals | Human-approved specs and edits on record; SBOM and vulnerability-handling features |

---

## 8. Validation plan (Phase 0, 4–6 weeks; can start this month)

1. **12 design partners:** 5 solo technical founders, 4 small teams, 3 agencies. All real repositories; read-only connection first.
2. **Run a concierge factory** on Paperclip plus Claude Code/Codex for lines L2 (bugs) and L3 (maintenance), then L1 (features). We operate it by hand where the product doesn't exist yet.
3. **Measure:**
   - first-pass merge rate;
   - false-green rate;
   - change-failure rate;
   - cost per merged change;
   - review time per change;
   - hours saved.
4. **Pricing:** willingness to pay (Van Westendorp survey), plus a paid pilot at the outcome price (S $3 / M $12). Does anyone choose bring-your-own key?
5. **Go/no-go for the full rewrite and build:**
   - first-pass merge rate ≥ 50%;
   - zero false-green;
   - Medium cost ≤ $6;
   - ≥ 40% of partners "very disappointed" if it went away;
   - ≥ 6 of 12 willing to pay at the tested price.

---

## 9. Decisions for you

| # | Decision | Options | My recommendation |
|---|---|---|---|
| **D1** | Target customer | A enterprise · B non-technical founders · **C small software companies (solo technical founders, teams ≤ 20, agencies)** · D open-source control plane | **C**, then expand to A; use D as a channel |
| **D2** | Core message | "Replace engineers" · **"Engineers run the factory" / "Run a software company of one"** | The second. Keep "replace" as your personal belief, not a product claim |
| **D3** | What happens to "One Person Company" | Keep as the category · **keep as an audience phrase ("one-person software company")** · drop | Audience phrase only |
| **D4** | Foundation | From scratch (current PRD) · **Paperclip fork for the control plane** · hybrid | Paperclip fork |
| **D5** | Pricing model | Credits · per seat · **outcome price per merged change plus a small platform fee, with bring-your-own key as an option** | Outcome pricing, validated in Phase 0 |
| **D6** | Autonomy at launch | Level 5 lights-out · **Level 4, with lights-out earned per line** | Level 4 |
| **D7** | Launch date | **Keep W0 (week of 25 Jan 2027) as a public beta with lines L2 + L3 (+ L1 preview), only if D4 = Paperclip** · move to April 2027 | Keep W0 if on Paperclip; otherwise April |
| **D8** | Documents | **New dated folder plus "superseded" banners on the OPC docs** · rewrite in place | New folder |
| **D9** | Parked OPC features (front office, revenue loop, content engine, property kit) | **Park in an appendix** · delete | Park. They may return as a later "run the business" layer |

---

## 10. After you approve: the update plan

In this order, each document cross-linked as before:

1. `market-research.md` v3. The evidence base comes first, because everything else cites it.
2. `factory-lines.md`, replacing `industry-kits.md`.
3. `reliability-cost-harness.md` v2: the factory harness and cost model.
4. `product-feature-strategy.md` v2: VOC, bets F1–F7, backlog, roadmap.
5. `prd.md` v2: modules, architecture, delivery plan per D4 and D7.
6. `marketing-plan.md` v2: channels, launch, budget, copy.
7. `x-build-in-public-guide.md` v2.
8. README index and "superseded" banners.

Any decision you change in §9 flows into all of them. If you approve as recommended, no further research is needed before rewriting except for the extra VOC sources (GitHub issues, Hacker News, Reddit) noted in §5.5.

---

## Sources

- Concept: [Simon Willison on the five levels](https://simonwillison.net/2026/Jan/28/the-five-levels/) · [StrongDM Software Factory](https://simonwillison.net/2026/Feb/7/software-factory/) · [8090 pricing and modules](https://rywalker.com/research/8090-software-factory) · [EY and 8090](https://www.ey.com/en_us/newsroom/2026/03/ernst-young-llp-and-8090-launch-ey-ai-pdlc) · [Factory raises $200M](https://devops.com/factory-raises-200m-as-it-builds-agents-across-the-software-lifecycle/) · [AWS frontier agents](https://aws.amazon.com/blogs/machine-learning/aws-launches-frontier-agents-for-security-testing-and-cloud-operations/)
- Market: [JetBrains AI agent adoption 2026](https://blog.jetbrains.com/research/2026/08/ai-coding-agent-adoption-2026/) · [CNBC: SpaceX–Cursor](https://www.cnbc.com/2026/06/16/spacex-spcx-cursor-acquisition-ipo.html) · [Dealroom: Cursor $4B](https://dealroom.co/news/134107-cursor-tops-4b-annualized-revenue/) · [VentureBeat: Anthropic and Claude Code run rate](https://venturebeat.com/technology/anthropic-says-it-hit-a-30-billion-revenue-run-rate-after-crazy-80x-growth) · [Bloomberg: Cognition $48B](https://www.bloomberg.com/news/articles/2026-09-08/ai-startup-cognition-raises-2-billion-at-a-48-billion-value) · [Lovable Series C](https://lovable.dev/blog/series-c) · [Sacra: Replit](https://sacra.com/c/replit/) · [Microsoft FY26 Q2](https://www.microsoft.com/en-us/investor/events/fy-2026/earnings-fy-2026-q2) · [Cursor: Gartner MQ 2026](https://cursor.com/blog/cursor-leads-gartner-mq-2026) · [Enterprise DNA: Gartner market size (secondary)](https://enterprisedna.co/resources/news/gartner-enterprise-ai-coding-agents-10-billion-market-2026/) · [Stripe: solo founders](https://stripe.com/blog/top-solo-founder-traits) · [HSEP: Carta solo founders](https://hsep.substack.com/p/solo-founders) · [Bloomberg: Resolve AI](https://www.bloomberg.com/news/articles/2026-02-04/resolve-ai-hits-1-billion-valuation-for-outage-thwarting-ai-agents) · [DevOps.com: Cursor acquires Graphite](https://devops.com/cursor-acquires-graphite-to-streamline-ai-powered-development/) · [VKTR: Claude Code Review](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/)
- Pricing: [Devin pricing (secondary)](https://www.usecarly.com/blog/devin-pricing/) · [Factory pricing (secondary)](https://continuumcode.ai/guides/factory-ai-pricing/) · [Claude API pricing](https://platform.claude.com/docs/en/about-claude/pricing) · [Claude Code costs](https://code.claude.com/docs/en/costs) · [GitHub: Copilot usage-based billing](https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/) · [The Register: Copilot backlash](https://www.theregister.com/ai-and-ml/2026/06/02/github-copilot-users-threaten-exit-as-metered-billing-kicks-in/5249826) · [Forbes: Uber AI budget](https://www.forbes.com/sites/janakirammsv/2026/05/17/uber-burns-its-2026-ai-budget-in-four-months-on-claude-code/)
- Reliability and risk: [METR time horizons](https://metr.org/time-horizons/) (raw data `benchmark_results_1_1.yaml`) · [DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/) · [CodeRabbit AI vs human code](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report) · [Veracode 2026](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/) · [Anthropic 2026 Agentic Coding Trends Report](https://resources.anthropic.com/2026-agentic-coding-trends-report) · [ADTmag: Stack Overflow survey](https://adtmag.com/blogs/watersworks/2026/01/stack-overflow-survey.aspx) · [Tom's Hardware: PocketOS](https://www.tomshardware.com/tech-industry/artificial-intelligence/claude-powered-ai-coding-agent-deletes-entire-company-database-in-9-seconds-backups-zapped-after-cursor-tool-powered-by-anthropics-claude-goes-rogue) · [CSA: vibe-coding security debt](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/) · [METR RCT follow-up (secondary)](https://ingenire.com/blog/metr-2026-developer-productivity-study)
- Jobs and labor: [Indeed Hiring Lab](https://hiringlab.indeed.com/2026/07/08/ai-and-job-postings-from-destruction-to-creation/) · [BLS: software developers, QA analysts and testers](https://www.bls.gov/ooh/computer-and-information-technology/software-developers.htm)
- Regulation and IP: [European Commission: CRA reporting](https://digital-strategy.ec.europa.eu/en/policies/cra-reporting) · [Library of Congress: Copyright Office AI report, Part 2](https://newsroom.loc.gov/news/copyright-office-releases-part-2-of-artificial-intelligence-report/s/f3959c36-d616-498d-b8f9-67641fd18bab)
- Primary data pulled for this proposal: Trustpilot business pages for lovable.dev, replit.com, base44.com, emergent.sh, bolt.new, cursor.com and windsurf.com (rendered 2026-10-04) · Census [SUSB 2021](https://www2.census.gov/programs-surveys/susb/datasets/2021/) and NES 2023 · Google Trends (pytrends, 2025-01-01 to 2026-10-03) · [Paperclip on GitHub](https://github.com/paperclipai/paperclip) · [Webvise: Paperclip adoption](https://www.webvise.io/blog/paperclip-ai-company-orchestration)

## Method notes

- **Review coding** used keyword rules per theme, with themes allowed to overlap, followed by a manual spot-check of samples. "Paid for failure" means a review mentions both credits or usage and an error, loop or broken fix. A detector for "claimed done but wasn't" was too noisy to report.
- **Sizing** is order-of-magnitude only. SUSB 2021 is the latest firm-size file published. Census NES 2023 counts businesses, not people.
- **Cost per change** is a model built from list prices and token assumptions, cross-checked against Anthropic's published enterprise averages. Phase 0 must replace it with measured data.
- **Secondary sources** (aggregators, press summaries) are labeled; where a primary source exists it is linked instead.
