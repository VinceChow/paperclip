# Competitor Analysis: Factory (factory.com) and the Software-Factory Field

**Date:** 2026-10-04
**Part of:** [Market research v3](./market-research.md) · [Product strategy v2](./product-feature-strategy.md) · [Marketing plan v2](./marketing-plan.md) · [PRD v2](./prd.md)
**Question:** Who else is building an AI software factory, especially Factory (factory.com, formerly factory.ai)? What do they offer and charge? Where do they overlap with our plan, and what should we change?

**Method:**
- **Factory:** product, pricing, enterprise, security and news pages rendered in a headless browser (2026-10-04). Also 28 documentation pages read in raw Markdown (pricing, Software Factory, QA, code review, security review, incident response, release, automations, Missions, autonomy, permission rules, sandbox, Droid Shield, router, bring-your-own-key, Agent Readiness, Agent Effectiveness), plus the changelog.
- **Other vendors:** pricing pages for Devin, Cursor, GitHub Copilot, Augment, Amp, Kiro, Claude, Jules, 8090 and Tessl, rendered the same day.
- **Press and primary sources** for funding, revenue and launches.
- **Developer comments:** Hacker News comments mentioning Factory and Droid since January 2025 (137 matched; only a handful were about Factory, most were about F-Droid).

Feature claims marked "Private Preview" come from the vendor's own docs. "Not found" means we found no public documentation, not that the feature doesn't exist.

---

## 1. Summary

1. **Factory is now our closest competitor, and it uses our category name.** Since the domain move, factory.com's headline is "**Build your software factory.**" It already ships, or previews, most of the factory stations we planned:
   - repository readiness scoring;
   - a living repository wiki;
   - a model router plus bring-your-own-key;
   - automations (ticket to PR, code health, error triage, CI-failure triage);
   - code review, security review, browser-based QA, incident response and release gates;
   - Missions (planned multi-feature work with validator workers).
   
   It also has a **self-serve Teams plan for small teams: $60 a month plus $40 per seat, up to 10 seats.** It raised $200M at $5B (Sep 2026) and ships CLI and desktop releases almost daily.
2. **But Factory sells a powerful toolkit priced like an agent, not a factory priced on outcomes.**
   - **Billing:** credits plus rolling 5-hour, 7-day and 30-day rate limits.
   - **Safety is configurable rather than structural:** autonomy levels Off to High; OS sandboxing exists but must be switched on; Missions require "High" autonomy.
   - **Enterprise-first:** the whole-lifecycle "Software Factory" dashboard, Release, Incident Response and Agent Effectiveness are all **Private Preview**, aimed at enterprise accounts.
3. **Cognition (Devin) has moved toward outcome pricing at the enterprise end.** Its "AI Productivity Guarantee" estimates the engineering hours each task saved and funds the shortfall in credits, up to $10M, at the end of an annual enterprise contract. Unmerged PRs count as no value. Cognition passed **$1B in annualized revenue** (25 Sep 2026). Its Teams plan is $80 a month plus $40 per seat.
4. **Orchestration is commoditizing.** Free or open-source "software factory" engines now exist:
   - **OpenAI's Symphony spec:** Linear issue → agent → PR with proof of work; 25K+ stars.
   - **Fabro:** "the open-source dark software factory for small teams of expert engineers."
   - **Warp Oz** (open-sourced) and **Amp** (free when you bring your own keys and compute).
   - **Paperclip,** our own base.
   
   A curated list now tracks 300+ such projects. Running agents in parallel against an issue tracker no longer differentiates anyone.
5. **What is still open,** and what we should lead with:
   - **pricing per merged change,** shown before work starts, with failed work free and a refund if the change breaks `main`. No self-serve competitor does this;
   - **safe by default:** sandboxes with no secrets, a separate merge identity, High-tier changes always going to a human;
   - **hidden holdout scenarios plus a public false-green rate;**
   - **a done-for-you factory for 1–20-person teams:** packaged lines and a weekly owner report instead of a toolkit to configure;
   - **guaranteed human support.**
   
   Model neutrality and a repository X-ray are now **expected features** that every competitor has, not differentiators (§7).

---

## 2. Factory (factory.com): deep teardown

### 2.1 Company

| Item | Detail | Source |
|---|---|---|
| Founded | 2023 | [DevOps.com](https://devops.com/factory-raises-200m-as-it-builds-agents-across-the-software-lifecycle/) |
| Funding | $150M Series C at $1.5B (Apr 2026); **$200M at $5B** (15 Sep 2026); more than $400M in total. Investors: Blackstone, Khosla, Sequoia, Insight, NEA and others | [Factory news](https://factory.com/news/5-billion-valuation) |
| Customers (named) | Nvidia, Adobe, Palo Alto Networks, T-Mobile, Blackstone, RBC; case studies from Comarch, You.com, Groq, Empower, Nav. "Used by hundreds of thousands of developers" | Same; [factory.com/enterprise](https://factory.com/enterprise) |
| Revenue | Not disclosed. Press reported revenue doubling monthly for six months in 2026 | Press |
| Distribution | Listed in the **OpenAI B2B marketplace** (29 Sep 2026) and the **Claude Marketplace** (9 Sep 2026); expanded to Japan | [Factory news](https://factory.com/news) |
| Pace | CLI and desktop releases almost daily (v0.233 on 3 Oct 2026) | [Changelog](https://docs.factory.com/changelog/release-notes.md) |
| Context | Public dispute with Cognition over a board adviser (30 Sep 2026); the two compete for the same enterprises | [TechCrunch](https://techcrunch.com/2026/09/30/factory-ceo-just-accused-his-vc-board-advisor-of-spying-for-cognition/) |

### 2.2 Product map

| Our factory station | Factory capability | Maturity |
|---|---|---|
| Intake | Remote delegations from Slack, Linear and Jira; **Triage** automation | Generally available / Private Preview (Triage) |
| Repo X-ray | **Agent Readiness:** 5 levels (Functional → Autonomous), `/readiness-report`, `/readiness-fix`, an org dashboard and an API | Generally available |
| Product Brain | **AutoWiki:** a living repository wiki, refreshed on every push | Generally available |
| Spec and plan | **Spec Mode** (read-only planning); **Missions:** a plan of features and milestones, orchestrated by Mission Control; "sweet spot about 1–500 features" | Generally available (Missions still "evolving") |
| Build | **Droid** in the desktop app, CLI, SDK and headless `droid exec`; **Droid Computers** (managed cloud machines, or bring your own) | Generally available |
| Verify | `/review` and **Automated Code Review** (GitHub Action/GitLab); **Security Review** (STRIDE/OWASP); **Automated QA** (generated per-repository QA skills that test the app "as a real user would", with visual evidence); Mission validator workers at each milestone | Generally available (QA) |
| Release | **Release:** deployment gates, readiness and post-ship feedback | **Private Preview** |
| Operate | **Incident Response** (Slack alerts → investigation → fix PR); automations for error triage and CI-failure triage | **Private Preview** (Incident Response); automations generally available |
| Maintenance | Automation starters: "Code Health" (dependency audits, dead code, coverage, docs, one small PR per run), "Review Comment Fixer", "New Issue Investigator" | Generally available (Automations, 30 Sep 2026) |
| Factory view | **Software Factory** dashboard: coverage by stage (Triage, Code-gen, Validate, Release, Document, Monitor) | **Private Preview** |
| Measurement | **Analytics** (2 Oct 2026); **Agent Effectiveness** (cycle time against agent spend, attribution) | Generally available / **Private Preview** |
| Models | **Factory Router:** "63% aggregate cost savings" against frontier-model rates, and 99% of Opus 4.7's pass rate on Terminal-Bench 2. **Bring your own key,** including local and open-weight models; Droid Core free pool | Generally available |
| Safety | Autonomy levels (Off / Low / Medium / High); permission rules (allow / ask / block); **OS sandbox** (Seatbelt on macOS, bubblewrap on Linux, domain-filtering proxy) once enabled in settings; **Droid Shield** secret scanning on commit and push (Droid Shield 2.0 in Private Preview); hooks | Generally available |
| Enterprise | SSO/SAML/SCIM, audit logs, zero data retention, data residency, **Factory Private** (your own VPC, on-premises or air-gapped), FedRAMP in progress, SOC 2, ISO 42001 | Generally available |
| Benchmarks | Agent Arena, Legacy-Bench (joined Fireworks' index), Review Benchmark, Terminal-Bench, Next.js evals | Published |

### 2.3 Pricing (factory.com/pricing and docs, 2026-10-04)

| Plan | Price | What you get |
|---|---|---|
| Pro | $20 / month | App, CLI, SDK; cloud and local background agents; readiness dashboard |
| Plus | $100 / month | About 5x Pro usage; Factory-managed Droid Computers |
| Max | $200 / month | About 10x Pro usage; early access |
| **Teams** | **$60 / month per team + $40 / month per seat** | Pro rate limits per seat; **up to 10 seats**; centralized billing |
| Business | Custom | Custom limits; SSO/SAML/SCIM; zero data retention; audit logs; admin controls (models, autonomy, deny lists, network policy) |
| Enterprise | Custom | Unlimited seats, dedicated compute, on-premises, data residency, readiness program |

**How usage works:**
- Sessions consume **Factory Standard Credits** by model, plus compute for Droid Computers.
- Individual plans have **three rolling rate limits** (5-hour, 7-day, 30-day).
- When those run out, you can switch to the free Droid Core model pool or buy **Extra Usage** (prepaid, $10 minimum).
- Missions require Extra Usage to be enabled, and pause when a rate limit hits.

So the customer pays for **consumption**, including failed attempts.

### 2.4 Strengths

1. **The broadest lifecycle coverage of any self-serve product.** Nearly every station we planned exists in some form.
2. **Engineering-grade harness.** Developers rate it highly: "the coding agent I trust enough to go all-in" ([Every](https://every.to/vibe-check/vibe-check-i-canceled-two-ai-max-plans-for-factory-s-coding-agent-droid)). On Hacker News: "same model … works better in 3P harnesses such as Factory Droid or Amp."
3. **Cost engineering:** the router claims 63% savings; bring-your-own-key; a free open-weight pool.
4. **Enterprise trust:** air-gapped deployment, ISO 42001, marketplace listings with OpenAI and Anthropic.
5. **Speed of execution:** near-daily releases; launched Automations, Analytics, Router and Factory Private within three weeks.
6. **Category ownership:** it uses the "software factory" language, and has the brand "Factory."

### 2.5 Weaknesses and openings for us

| Gap | Evidence | Our answer |
|---|---|---|
| **Consumption pricing** | Credits, three rolling rate limits, prepaid Extra Usage; Missions pause on limits | Price per merged change, quoted before work; failed work free; refund on false green |
| **Safety is opt-in and per-session** | The sandbox has to be enabled in settings; Missions "require High autonomy or `--skip-permissions-unsafe`"; agents run on the developer's machine with local credentials by default | Safe by default: sandbox-only builds with no secrets, a separate merge identity, High tier always individual |
| **Verification is generated, not held out** | QA skills are generated from the codebase; Mission validators check milestones. No hidden holdout scenarios or post-merge false-green accounting found | Holdout scenarios hidden from the builder; 7-day false-green audit; published rate |
| **The whole-factory layer is enterprise and preview** | Software Factory dashboard, Release, Incident Response and Agent Effectiveness are Private Preview, via the account team | A done-for-you factory for 1–20-person teams, self-serve on day one |
| **Complexity** | Docs cover 100+ pages: autonomy levels, permission rules, hooks, skills, plugins, Missions, computers, templates and more | Lines with defaults; a three-question onboarding; Advanced hidden |
| **Missions still "evolving"** | Their docs list open questions on parallelism, correctness over long plans, and cost versus quality; a user calls Missions' verification "overdoing mandatory verification steps" | Order sizing from measured pass rates; small orders instead of long missions |
| **No outcome guarantee** | None published (Cognition has one; §3.1) | Per-change charging and false-green refunds |

### 2.6 What we should borrow (ideas, not code)

- **Agent Readiness levels** as a shared language. Map our Repo X-ray to a simple 1–5 "factory-ready" score, with "fix it" orders.
- **Guided setup flows** (`/install-qa`, `/install-code-review`) that generate checked-in configuration the customer owns.
- **A generous free fallback model pool,** so work doesn't stop when budgets run out (for us: queue for approval rather than stop).
- **Public benchmarks across several dimensions,** including legacy code and review quality. Ours should measure what theirs doesn't: **cost per verified change and false-green rate.**

---

## 3. Other competitors

### 3.1 Cognition (Devin + Windsurf)

| Item | Detail |
|---|---|
| Scale | **$1B+ annualized revenue** (25 Sep 2026); $2B raised at $48B (Sep 2026) ([Cognition](https://cognition.com/blog/1b-run-rate), [Bloomberg](https://www.bloomberg.com/news/articles/2026-09-08/ai-startup-cognition-raises-2-billion-at-a-48-billion-value)) |
| Product | Devin cloud agents; **Devin Desktop** (IDE plus an agent command center with a Kanban of local and cloud agents); **Devin Review** (PR analysis, vulnerability flags); **DeepWiki**; desktop end-to-end testing by computer use; scheduled Devins; **Fusion** (a frontier "lead" model plus a cheap "sidekick" model); its own SWE-2 model ([Devin docs](https://docs.devin.ai/release-notes/2026)) |
| Pricing | Free; Pro $20; Max $200; **Teams $80 a month + $40 per full seat (up to 200 users)**; Enterprise ([devin.ai/pricing](https://devin.ai/pricing)) |
| Outcome promise | **AI Productivity Guarantee:** a value estimator converts each session's productive hours to dollars at a standard rate. If value is below spend, credits are issued near the end of the annual contract, up to $10M. Unmerged or unproductive sessions count as no value. Enterprise only ([Cognition](https://cognition.com/blog/ai-guarantee)) |
| Benchmark | **FrontierCode:** "would a maintainer actually merge this PR?" |
| Threat to us | **High.** Strong brand, self-serve Teams plan, outcome narrative. **Opening:** the guarantee is enterprise, annual and paid in credits. Ours is self-serve, per change, immediate, and refunds false greens |

### 3.2 8090 (Software Factory)

| Item | Detail |
|---|---|
| Product | "8090 Software Factory®": Requirements, Blueprints, Work Orders (executed in Cursor, VS Code or Claude Code), Feedback; trial at factory.8090.ai; services-led modernization (for example 18M+ lines of COBOL at CMS) ([8090](https://www.8090.ai), [8090 Software Factory](https://www.8090.ai/software-factory)) |
| Pricing | $200 per user per month plus tokens; enterprise from $1M a year (secondary: [Ry Walker](https://rywalker.com/research/8090-software-factory)) |
| Naming | USPTO application for **"8090 SOFTWARE FACTORY"** (filed 16 Jul 2025, intent to use; [uspto.report](https://uspto.report/TM/99287889)). The site shows ® |
| Threat | **Low** for small teams (enterprise, services-led). **Medium** for naming |

### 3.3 Labs and platforms (the "do it yourself" substitute)

| Product | What it now includes | Price | Threat |
|---|---|---|---|
| **Claude Code** (Anthropic) | CLI, IDE, web and desktop; multi-agent **Code Review** (about $15–25 per review); GitHub Actions; Managed Agents ($0.08 per session-hour plus tokens) | Pro $20; Max $100/$200; Team; Enterprise $20 per seat + API usage ([claude.com/pricing](https://claude.com/pricing)) | **Very high as a substitute.** It's what most developers already use (39%) |
| **Codex** (OpenAI) | Cloud tasks with reusable environments; automatic code reviews; security scans (DevDay 2026); **Symphony** open spec | Plus $20; Pro; Business $20–25 per user; Codex-only credit seats ([OpenAI](https://developers.openai.com/codex/pricing), [The Decoder](https://the-decoder.com/openai-expands-codex-and-its-api-at-devday-with-security-scans-a-decisions-api-and-ultrafast/)) | **Very high as a substitute** |
| **GitHub Copilot** | Cloud agent (issue → PR); **delegates to Claude Code and Codex**; code review; Agent HQ | $10 / $39 / $100 tiers with included AI Credits; Business and Enterprise ([GitHub](https://github.com/features/copilot/plans)) | **High:** distribution inside GitHub |
| **Cursor** (SpaceX) | Cloud agents; **Automations** (schedule, Slack, Linear, GitHub, PagerDuty, Sentry, webhooks; March 2026); **Bugbot** plus **Bugbot Autofix** (GA Feb 2026); Graphite | Pro $20; Teams $40 per user ([Cursor](https://cursor.com/pricing), [changelog](https://cursor.com/changelog/03-05-26)) | **High** |
| **Google** | Jules (cloud VM, runs tests, PRs; 15 tasks a day free); Antigravity 2.0 agent teams | Free tiers; AI Pro $19.99 ([jules.google](https://jules.google)) | Medium |
| **AWS** | Kiro (spec-driven IDE) plus autonomous agent (preview); Security Agent and DevOps Agent (GA 31 Mar 2026) | Kiro $20–200 per user in credits ($0.04 per extra credit) ([kiro.dev](https://kiro.dev/pricing)) | Medium (AWS-centric) |

### 3.4 Team-oriented agent platforms

| Product | Notes | Price | Threat |
|---|---|---|---|
| **Augment Cosmos** (May 2026) | "Unified agents platform for software teams": shared context and memory; Prism routing; bring-your-own-key; reference experts for Deep Code Review, PR Author, E2E Testing and Incident Response ([SiliconANGLE](https://siliconangle.com/2026/06/05/augment-code-launches-cosmos-bring-agentic-ai-software-development-teams/)) | **$20 a month flat for up to 50 seats** with $20 of usage; Business $100 flat ([pricing](https://www.augmentcode.com/pricing)) | **Medium–high:** aggressive small-team price |
| **Amp** (Sourcegraph spin-out) | "Orbs": remote machines per thread, previews ("portals"), review from anywhere; a demo shows granting an orb **production access** | $20 / $200, or **free with your own keys and compute** since 13 Sep 2026 ([ampcode.com](https://ampcode.com), [AICoder](https://aicoder.com/news/news-20260912-amp-byok-free)) | Medium |
| **Warp Oz** | Orchestration for cloud agents; multi-harness (Claude Code, Codex, Warp); open-sourced April 2026 | Free; Build $18; Business $45; Max $180 (credits) ([Warp](https://www.warp.dev/newsroom/2026/3/22/warp-reaches-one-million-active-users-launches-oz-cloud-platform)) | Medium |
| **Tessl** | "Build your software factory, one skill at a time": a skills registry, loops (review, security, docs, evals, cost benchmarking) | 1,000 free credits a month ([tessl.io](https://tessl.io)) | Low–medium |

### 3.5 Open-source factories (they commoditize orchestration)

| Project | What it is | Notes |
|---|---|---|
| **OpenAI Symphony** | Spec plus Elixir reference implementation: Linear issue → isolated workspace → agent → PR with **proof of work** (CI status, walkthrough) → human review. Apache 2.0 | 25K+ stars; OpenAI says it won't maintain it as a product ([OpenAI](https://openai.com/index/open-source-codex-orchestration-symphony/)) |
| **Fabro** (Qlty Software) | "The open-source dark software factory for small teams of expert engineers": workflow graphs in Graphviz DOT; builds and tests as gates; cloud sandboxes with network controls; human approval gates; multi-model routing; MIT | Closest open-source analogue to our concept ([fabro.sh](https://fabro.sh/)) |
| **Gas Town, addyosmani/factory, Vercel "eve" template, Ramure (formerly Druids), MartinLoop** | Orchestrators and templates; MartinLoop adds budget caps, verification gates and "signed receipts" | Listed in [awesome-software-factories](https://github.com/varun1505/awesome-software-factories) (300+ projects) |
| **Paperclip** (our base) | Agent control plane, MIT, about 47K stars | — |

**Implication:** an open-source engine is table stakes, and it's our starting point too. Customers pay for **outcomes, safety, evidence, economics and support,** not for orchestration.

### 3.6 App builders and point tools

- **App builders** (Lovable, Replit, Bolt, Base44, Emergent): a different buyer. Their reviews punish money and support issues (see [market research §4.4](./market-research.md#44-voice-of-customer-656-negative-reviews-trustpilot)). They overlap only with our L4 Greenfield line.
- **Point tools** (CodeRabbit, Greptile, Qodo; Snyk, Semgrep; Resolve AI, Traversal): integrate them or out-bundle them. Each one covers a single station.

---

## 4. Feature comparison (self-serve plans for small teams)

✓ = generally available and documented · ◐ = preview, partial or enterprise-only · ✗ = not found · ? = not verified.

| Capability | **[Brand] (plan)** | Factory | Devin | Cursor | Copilot | Claude Code | Augment | Fabro (OSS) |
|---|---|---|---|---|---|---|---|---|
| Background or cloud agents | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Model choice / bring your own key | ✓ | ✓ | ✓ | ✓ | ✓ (delegates to Claude and Codex) | ✗ (Claude only) | ✓ | ✓ |
| Repository readiness / X-ray | ✓ | ✓ (Agent Readiness) | ? | ✗ | ✗ | ✗ | ? | ✗ |
| Living repository knowledge | ✓ (Product Brain) | ✓ (AutoWiki) | ✓ (DeepWiki) | ◐ | ◐ | ◐ | ✓ (Context Engine) | ✗ |
| Scheduled and event automations | ✓ (lines) | ✓ | ✓ (scheduled) | ✓ | ◐ | ◐ | ✓ | ✓ (workflows) |
| AI code review | ✓ (part of verify) | ✓ | ✓ | ✓ (Bugbot) | ✓ | ✓ | ✓ | ◐ |
| Security review / scans as gates | ✓ | ✓ | ◐ | ◐ | ◐ | ◐ | ? | ◐ |
| End-to-end / user-flow QA | ✓ (holdouts on preview) | ✓ (generated QA skills) | ✓ (desktop testing) | ◐ | ✗ | ◐ | ✓ (E2E expert) | ◐ |
| **Hidden holdout scenarios** | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Post-merge false-green audit plus refund** | ✓ | ✗ | ◐ (enterprise guarantee) | ✗ | ✗ | ✗ | ✗ | ✗ |
| Incident response | P1 | ◐ (preview) | ? | ✓ (automations) | ✗ | ✗ | ✓ (expert) | ✗ |
| Release gates / rollback | P1 | ◐ (preview) | ✗ | ✗ | ✗ | ✗ | ? | ◐ |
| **Isolated cloud sandbox by default** | ✓ (and no secrets) | ◐ (local by default; opt-in OS sandbox; managed computers optional) | ✓ (cloud VM) | ✓ (cloud agents) | ✓ (Actions-based) | ◐ (local by default; cloud option) | ◐ | ✓ |
| **Separate merge identity / tier policy** | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ◐ (approval gates) |
| Lights-out earned per line | ✓ | ✗ (autonomy levels) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Pricing unit** | **Per merged change** | Credits + rate limits | Quota / usage | Seats + usage | Seats + AI credits | Subscription windows / API | Flat + usage | Free (your infrastructure) |
| Small-team self-serve plan | ✓ | ✓ ($60 + $40 per seat) | ✓ ($80 + $40 per seat) | ✓ ($40 per user) | ✓ | ✓ | ✓ ($20 flat) | ✓ (DIY) |
| Guaranteed human support response | ✓ (≤ 1 business hour Team and Agency) | ◐ (enterprise) | ◐ (Teams "priority") | ◐ | ◐ | ◐ | ◐ | ✗ |

---

## 5. Price comparison for a 5-person team (list prices, monthly)

| Product | Team price | Usage model | Notes |
|---|---|---|---|
| Factory Teams | $60 + 5 × $40 = **$260** | Pro rate limits per seat; extra usage prepaid | Software Factory layer is enterprise preview |
| Devin Teams | $80 + 5 × $40 = **$280** | Per-seat quota; extra at API prices | Guarantee is enterprise only |
| Cursor Teams | 5 × $40 = **$200** | Included usage plus usage-based | Bugbot, automations |
| Augment Standard | **$20 flat** (up to 50 seats) | $20 of usage included; pay as you go | Cosmos included |
| Claude Team (Standard) | ≈ 5 × $25–30 = **$125–150** | Usage windows; Premium seats for heavy coding | Code Review is extra per review |
| Copilot Business | 5 × $19 = **$95** | AI credits; usage beyond | Cloud agent delegates to Claude and Codex |
| **[Brand] Team** | **$199** (5 seats) **+ $3 / $12 per merged change** | Outcome-priced; failed work free; cap | About $1,159 at 80 Medium changes |

**Reading:**
- At list price, our platform fee is in line with the market. The **per-change fee** is the visible difference, and it must be justified by:
  - no review burden (the evidence card);
  - no failed-work cost;
  - safety;
  - support.
- Heavy users comparing against "Claude Max at $200 a month" will see us as expensive per unit. Our pitch is cost per **merged, verified** change, not cost per token.
- **Action:** in Phase 0, test a bundle (for example the Solo plan includes 10 Medium changes) against pure per-change pricing.

---

## 6. Threat ranking for our wedge (small software companies)

| Rank | Competitor | Threat | Why | Watch for |
|---|---|---|---|---|
| 1 | **Factory** | **Very high** | Same category language; small-team plan; broadest coverage; fast shipping | Software Factory dashboard and Release leaving Private Preview; any outcome-based pricing; small-team packaging |
| 2 | **Claude Code / Codex, do it yourself** | **Very high (substitute)** | Already in every developer's hands; cheap subscriptions; Symphony shows the do-it-yourself path | A lab ships managed "factory mode" with verification |
| 3 | **Cognition (Devin)** | High | $1B+ run rate; Teams plan; outcome guarantee narrative | The guarantee extended to Teams |
| 4 | **Cursor** | High | Teams $40; automations; Bugbot Autofix | Automations plus Bugbot packaged as "maintenance" |
| 5 | **GitHub Copilot** | High | Distribution; delegates to Claude and Codex | Agent HQ with gates and merge policies |
| 6 | **Augment Cosmos** | Medium–high | $20 flat for 50 seats | Price pressure on small teams |
| 7 | Amp, Warp Oz, open-source factories (Fabro, Symphony) | Medium | Free or open source; good for experts | Hosted versions with verification |
| 8 | Google, AWS | Medium | Free or cheap tiers; cloud ties | — |
| 9 | 8090 | Low (product) / Medium (naming) | Enterprise, services-led | Trademark enforcement on "Software Factory" |
| 10 | App builders, point tools | Low–medium | Different buyer or a single station | Lovable's "help people run their businesses" push |

---

## 7. What this changes in our plan (recommendations)

These recommendations follow from the evidence. Items marked **(decision)** need your approval before the other documents change. The other items are corrections already applied to the plan set (§9).

| # | Recommendation | Why |
|---|---|---|
| C1 | **Demote model neutrality and the Repo X-ray to expected features** (keep building them; stop selling them as differentiators) | Factory (Router, bring-your-own-key, Agent Readiness), Augment (Prism), Copilot (delegation), Warp Oz and Amp all have them |
| C2 | **Lead with the economic model:** "priced per merged change, before work starts; failed work free; refund if it breaks main" | Only Cognition has an outcome promise, and it's enterprise, annual and paid in credits. Factory, Cursor, Copilot and Kiro bill consumption |
| C3 | **Make "safe by default" a headline proof point** (sandbox with no secrets, separate merge identity, High tier always human) | Factory's sandbox is opt-in and Missions need High autonomy; Amp demos granting production access |
| C4 | **Position against toolkits:** "the factory you don't have to build" for 1–20-person teams. Lines with defaults, three-question onboarding, a weekly owner report | Factory's docs span 100+ configuration pages; its factory layer is enterprise preview |
| C5 | **(decision) Category wording:** keep "AI software factory" as a descriptive phrase in content, but lead headlines with "**verified software factory**" or "**verified changes**", and get counsel before using "Software Factory" in any product name | Factory's headline is "Build your software factory"; Tessl uses similar wording; 8090 has a USPTO application for "8090 SOFTWARE FACTORY" |
| C6 | **Differentiate the benchmark:** measure *cost per verified change* and *false-green rate*, not model pass rates | Factory (Agent Arena, Legacy-Bench, Review Benchmark) and Cognition (FrontierCode) already own leaderboard-style benchmarks |
| C7 | **(decision) "Bring your agent" posture:** let customers run Droid, Devin, Claude Code or Codex as the build station inside our factory where their terms allow, and sell the verification, safety and economics layer around them | Neutralizes "my team already uses X"; Paperclip already has adapters for Claude Code, Codex, Cursor and others |
| C8 | **Pricing test:** add a bundle variant (for example 10 Medium changes included in Solo) to the Phase 0 price test | Competitors' flat seats plus included usage; Augment at $20 flat |
| C9 | **Competitive watch:** a monthly check of Factory's changelog and maturity tags, Cognition's guarantee terms, and Cursor and Copilot automations | Fast-moving field; Factory ships almost daily |

---

## 8. Battlecards

### vs Factory
- **They say:** "Build your software factory." Droids across the lifecycle; enterprise-grade.
- **We say:** "Factory gives you the parts to build a factory. We run one for you, and you pay only for changes that merge."
- **Proof points:**
  - per-change pricing, failed work free, false-green refund;
  - sandbox-only builds with no secrets and a separate merge identity;
  - hidden holdout scenarios;
  - live in 30 minutes with no configuration;
  - a human reply within 1 business hour.
- **Concede:**
  - Factory's harness and breadth are excellent;
  - enterprises needing air-gapped deployment should look at Factory.

### vs Devin
- **They say:** an autonomous engineer, with a $10M productivity guarantee.
- **We say:** "Same idea, but self-serve and per change. You see the price before work starts, and a broken change is refunded within 7 days, not as credits at the end of an annual contract."

### vs Claude Code or Codex (do it yourself)
- **They say:** "I already have Claude Max or Codex. Why pay more?"
- **We say:** "Keep it. We add what a subscription doesn't:
  - tests first;
  - hidden scenarios;
  - scans and previews;
  - a merge identity that can't touch production;
  - a price per *verified* change;
  - a weekly report.
  
  Your evenings go to decisions, not reviews."

### vs Cursor or Copilot
- **They say:** cloud agents, automations, Bugbot, Agent HQ.
- **We say:** "Great for engineers in the editor. We're for the work you don't want to review line by line: bugs and maintenance with proof, merged on evidence."

### vs open-source factories (Fabro, Symphony, Paperclip)
- **They say:** "Free, and I control everything."
- **We say:** "We're built on open source too. You're paying for:
  - maintained lines;
  - holdout scenarios and twins;
  - the safety model;
  - outcome pricing;
  - a team that answers.
  
  If you'd rather run it yourself, the line format is open."

---

## 9. Corrections applied to the plan set (2026-10-04)

These fix statements that this research showed were no longer accurate. They don't change any approved decision.

| Document | Change |
|---|---|
| [Market research v3](./market-research.md) | Executive summary and §4: Factory's small-team plan and "software factory" positioning, Cognition's guarantee and $1B run rate, and the open-source factories added. Gaps 5 (small teams) and 6 (neutrality) restated honestly. Scorecard competition note updated |
| [Product strategy v2](./product-feature-strategy.md) | §1.4 baseline: model neutrality, repository readiness and automations moved to "expected features"; outcome pricing noted as enterprise-only elsewhere (Cognition) |
| [Marketing plan v2](./marketing-plan.md) | §2.4 one-liners: Factory and Devin lines updated; naming note on "Software Factory" (8090 trademark application) |
| [PRD v2](./prd.md) | §19.1 risks: Factory named as the primary competitive risk |
| [README](./README.md) | This document added to the index |

## Sources

- **Factory:**
  - [factory.com](https://factory.com) · [pricing](https://factory.com/pricing) · [enterprise](https://factory.com/enterprise) · [security](https://factory.com/security) · [news](https://factory.com/news) · [$5B round](https://factory.com/news/5-billion-valuation)
  - [Docs index](https://docs.factory.ai/llms.txt): [individual plans](https://docs.factory.com/pricing/individuals.md), [organization plans](https://docs.factory.com/pricing/organizations.md), [Software Factory](https://docs.factory.com/software-factory/overview.md), [Automated QA](https://docs.factory.com/software-factory/automated-qa.md), [code review](https://docs.factory.com/software-factory/code-review-ci.md), [Release](https://docs.factory.com/software-factory/release.md), [Incident Response](https://docs.factory.com/software-factory/incident-response.md), [Automations](https://docs.factory.com/software-factory/automations.md), [Missions](https://docs.factory.com/missions/overview.md), [autonomy level](https://docs.factory.com/autonomy-and-safety/auto-run.md), [sandbox](https://docs.factory.com/autonomy-and-safety/sandbox.md), [Droid Shield](https://docs.factory.com/autonomy-and-safety/droid-shield.md), [Factory Router](https://docs.factory.com/model-independence/factory-router.md), [Agent Readiness](https://docs.factory.com/agent-readiness/overview.md), [Agent Effectiveness](https://docs.factory.com/agent-effectiveness/overview.md), [changelog](https://docs.factory.com/changelog/release-notes.md)
  - Press and reviews: [DevOps.com](https://devops.com/factory-raises-200m-as-it-builds-agents-across-the-software-lifecycle/) · [TechCrunch](https://techcrunch.com/2026/09/30/factory-ceo-just-accused-his-vc-board-advisor-of-spying-for-cognition/) · [Every review](https://every.to/vibe-check/vibe-check-i-canceled-two-ai-max-plans-for-factory-s-coding-agent-droid)
- **Cognition:** [pricing](https://devin.ai/pricing) · [AI Productivity Guarantee](https://cognition.com/blog/ai-guarantee) · [$1B run rate](https://cognition.com/blog/1b-run-rate) · [Devin 2026 release notes](https://docs.devin.ai/release-notes/2026) · [Bloomberg](https://www.bloomberg.com/news/articles/2026-09-08/ai-startup-cognition-raises-2-billion-at-a-48-billion-value)
- **8090:** [8090.ai](https://www.8090.ai) · [Software Factory page](https://www.8090.ai/software-factory) · [USPTO application 99287889](https://uspto.report/TM/99287889) · [Ry Walker (pricing, secondary)](https://rywalker.com/research/8090-software-factory)
- **Labs and platforms:**
  - Anthropic: [Claude pricing](https://claude.com/pricing)
  - OpenAI: [Codex pricing](https://developers.openai.com/codex/pricing) · [The Decoder on DevDay](https://the-decoder.com/openai-expands-codex-and-its-api-at-devday-with-security-scans-a-decisions-api-and-ultrafast/) · [Symphony](https://openai.com/index/open-source-codex-orchestration-symphony/)
  - GitHub: [Copilot plans](https://github.com/features/copilot/plans)
  - Cursor: [pricing](https://cursor.com/pricing) · [Bugbot](https://cursor.com/bugbot) · [Automations](https://cursor.com/changelog/03-05-26)
  - Google and AWS: [Jules](https://jules.google) · [Kiro pricing](https://kiro.dev/pricing)
- **Team platforms:** [Augment pricing](https://www.augmentcode.com/pricing) · [SiliconANGLE on Cosmos](https://siliconangle.com/2026/06/05/augment-code-launches-cosmos-bring-agentic-ai-software-development-teams/) · [Amp](https://ampcode.com) · [Amp BYOK free](https://aicoder.com/news/news-20260912-amp-byok-free) · [Warp Oz](https://www.warp.dev/newsroom/2026/3/22/warp-reaches-one-million-active-users-launches-oz-cloud-platform) · [Tessl](https://tessl.io)
- **Open source:** [Fabro](https://fabro.sh/) · [awesome-software-factories](https://github.com/varun1505/awesome-software-factories)

## Method notes

- Feature marks come from each vendor's public pages and docs on 2026-10-04. Vendors ship weekly, so re-check before using any row in sales material, and never publish a competitor comparison without a dated source per row.
- Prices are list prices for self-serve plans. Enterprise prices are negotiated.
- Hacker News produced little developer feedback on Factory specifically: most "Droid" matches were F-Droid. The developer sentiment cited is qualitative.
- Trustpilot had no usable Factory or Devin reviews (§4.4 of the market research).
