# Product Strategy (v2): What the Factory Must Do to Win Small Software Companies

**Date:** 2026-10-04 (replaces the [OPC product feature strategy](../2026-09-26-opc-platform/product-feature-strategy.md))
**Author role:** Chief Product Officer
**Part of:** [Market research v3](./market-research.md) · [Competitor analysis](./competitor-analysis.md) · [Factory lines](./factory-lines.md) · [Factory harness](./reliability-cost-harness.md) · [PRD v2](./prd.md) · [Marketing plan](./marketing-plan.md)
**Question:** Which features make an AI software factory 10–100x better for solo founders, small teams and agencies than what they use today, and clearly different from the coding agents, platforms and app builders they could pick instead?

**Method:**
1. **Voice of customer, two sources:**
   - 656 negative and 246 positive Trustpilot reviews of seven AI-coding products;
   - 2,129 first-person Hacker News comments about coding agents (July–October 2026).
   
   Both were coded by theme ([market research §3.4, §4.4](./market-research.md#34-what-they-struggle-with-today-two-voice-of-customer-sources)).
2. **Evidence on how AI changes software delivery:** DORA, CodeRabbit, Veracode, METR, Anthropic and Stack Overflow.
3. **Competitor baseline:** labs, platforms, autonomous engineers, enterprise factories, app builders and point tools ([market research §4](./market-research.md#4-competitive-landscape-verified-2026-10-04)).
4. **Codebase review** of what Paperclip already provides ([harness §7](./reliability-cost-harness.md#7-paperclip-today-what-exists-vs-what-to-build)).

Where a number is a target or an estimate rather than measured data, it says so.

---

## 0. The decision on one page

**Product thesis.** Small software teams don't want *more code*. They want **shipped, safe, maintained software they can trust**, without hiring a platform team and without surprise bills.

Competitors compete on how much code an agent can write. Our customers struggle elsewhere:
- **reviewing and verifying** what agents produce (the top Hacker News theme, at 24%);
- **paying** for it (two-thirds of negative reviews);
- **keeping agents away from production;**
- **maintaining** what was built.

We win by changing two things:
- the **unit of value**, from *code* to **verified, merged changes**;
- the **interaction**, from *reading diffs* to **deciding on evidence**.

**The seven bets** (details in §3):

| # | Bet | The 10–100x outcome we will try to prove |
|---|---|---|
| F1 | **Zero-prompt start:** Repo X-ray plus Product Brain | Connect a repository → first merged, verified change in **≤ 30 minutes**, with no prompting |
| F2 | **Verified changes:** executable definition of done, tests first, holdout scenarios, twin services | **Zero false green**; first-pass merge rate ≥ 75% at GA |
| F3 | **Safe by construction:** sandboxes only, no production credentials, a gate on destructive actions | **0** production-credential exposures; 100% of High-tier changes approved by a human |
| F4 | **Decisions, not code reviews:** evidence inbox, batch approval, lights-out earned per line | Median review decision **≤ 60 seconds** per Medium change |
| F5 | **Predictable economics and real humans:** price before work, failed work free, caps, bring-your-own key, human support | **$0** paid for failed work; **0** surprise charges; human reply ≤ 1 business hour |
| F6 | **Operate what you ship:** previews, flags, staged rollout, rollback, regressions back as orders | Change-failure rate ≤ 10% at GA; time to restore ≤ 1 h for factory releases |
| F7 | **The weekly factory report:** DORA metrics, cost per change, **what failed and why** | ≥ 60% weekly open rate; it is the retention engine |

**What we won't build** (§9):
- "Replace your engineers" autopilot;
- agents with production credentials;
- credits or opaque usage meters;
- a new IDE;
- a general chat assistant;
- a no-code app builder for non-engineers;
- our own model.

**Scope:**
- **Public beta (W0, week of 25 Jan 2027):** S1–S19 in §6. About **69 person-weeks of engineering** on the Paperclip fork, about **80 person-weeks** with design, security and QA.
- **GA (late April 2027):** S20–S29, about 43 person-weeks.
- **Later:** S30–S36.

**North Star:** weekly merged, verified changes per active account.

**Customer-facing value metrics:**
- **engineering hours returned:** an estimate, with the method shown;
- **cost per change versus a human.**

---

## 1. What customers are telling us

### 1.1 Two voice-of-customer sources

| Theme | Trustpilot 1–2★ (656; mostly app-builder users) | Hacker News (2,129; mostly experienced engineers) |
|---|---|---|
| Money: credits, usage, billing, cost | **65.7%** (credits 48.6%, billing 41.6%) | 17.4% (cost, limits, pricing) |
| Support | 39.3% | — |
| Bugs, loops, "almost right" | 31.9% | 14.0% |
| Paid for failure | 24.4% | — |
| Review burden | — | **24.4%** |
| Context and large codebases | — | 16.8% |
| Tests and verification | — | 15.4% |
| Maintainability and "slop" | 11.9% (quality got worse) | 12.9% |
| Security and destructive actions | 8.1% (destructive) + 2.7% (security) | 9.8% |
| Productivity gains (positive) | 23% of positive reviews mention speed | 10.6% |

**What we take from the two sources:**
- **App-builder customers** punish unfair money and silence.
- **Engineers** are drowning in review and verification and worry about cost.
- No source says "we need a smarter model" as its top theme.
- Our bets target the top themes of both sources.

### 1.2 Where engineering time and money leak

| Leak | Evidence | Bet |
|---|---|---|
| Review is the new bottleneck | Code output per Anthropic engineer up about 200% in a year, making review the constraint ([VKTR](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/)). Review burden is the top Hacker News theme | F4 |
| AI changes need more fixing | About 1.7x more issues per PR ([CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report)); 66% of developers cite "almost right" code ([Stack Overflow 2025](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/)) | F2 |
| Speed without stability | AI raises throughput and change-failure rates ([DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/)) | F2, F6 |
| Security debt | 56% security pass rate ([Veracode](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/)); about 5,000 vibe-coded apps leaking data ([CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/)) | F2, F3 |
| Unpredictable bills | Enterprise average $150–250 per developer per month; power users $500–2,000; Uber spent its annual budget in four months; Copilot metered-billing backlash | F5 |
| Little true delegation | Developers fully delegate only 0–20% of tasks ([Anthropic](https://resources.anthropic.com/2026-agentic-coding-trends-report)) | F2, F4 |
| Destructive accidents | PocketOS production database and backups deleted in 9 seconds | F3 |

### 1.3 Why small teams stall with agents today

1. **No platform team.** DORA finds AI amplifies existing testing and delivery maturity. Small teams often lack strong tests, CI, previews and rollback, so AI makes them less stable, not more.
2. **Review overload.** One person can't read everything three agents write.
3. **Fear of production.** Agents run with the developer's own credentials and shell.
4. **Bills they can't forecast.** Usage meters punish exploration and failure.
5. **Context.** Agents don't know the architecture, conventions or "why," so output drifts.

### 1.4 What competitors already do (late-2026 baseline)

| Capability | Who has it | Status for us |
|---|---|---|
| Strong coding agents (CLI, IDE, cloud) | Claude Code, Codex, Cursor, Copilot, Devin, Antigravity | **Table stakes.** We integrate them as adapters; we don't compete with them |
| Background agents that open PRs | Copilot coding agent, Codex, Cursor, Devin, Jules | Table stakes |
| AI code review on PRs | Claude Code Review ($15–25 per review), CodeRabbit, Graphite, Copilot | Table stakes; ours is part of verification, not a separate product |
| Multi-agent "mission control" | GitHub Agent HQ; Factory Missions; Devin Desktop; Warp Oz and the Warp Factories Foreman; OpenAI Symphony and Fabro (open source); Paperclip | Table stakes (we have it via Paperclip) |
| Model routing and bring-your-own-key | Factory Router, Augment Prism, Copilot (delegates to Claude and Codex), Amp, Warp (any model or harness per factory agent) | **Table stakes.** Build it; don't sell it as a differentiator |
| Repository readiness scoring; living repository wiki | Factory (Agent Readiness, AutoWiki), Devin (DeepWiki), Augment (Context Engine) | **Table stakes.** Our Repo X-ray and Product Brain must match them, and use a simple 1–5 "factory-ready" score |
| Scheduled and event automations (ticket to PR, code health, error and CI triage) | Factory Automations (GA 30 Sep 2026), Cursor Automations, Devin scheduled runs, Augment Cosmos | **Table stakes.** Our lines must be better packaged and verified, not merely present |
| Security and SRE agents | AWS Security and DevOps agents, Snyk, Resolve AI | Integrate; take signals as intake |
| Factory measurement and self-improvement (cost per PR, autonomy rate, replay benchmarks on your own past work, self-improvement PRs against the factory definition) | **Warp Factories** (early access); Factory Agent Effectiveness (Private Preview) | **Must answer by P1.** Replay before line rollouts and line-improvement proposals (PRD ADM-7); autonomy and cost breakdown in the weekly report (RPT-7) |
| Lifecycle coverage ("software factory") | **Factory** (self-serve Teams at $60 + $40 per seat; whole-lifecycle layer in enterprise Private Preview); **Warp Factories** (factories-as-code infrastructure, priced per agent run, closed early access, aimed at smaller companies); 8090 (enterprise) | **Closest competitors.** We win on outcome pricing, safety by default, holdouts and false-green refunds, and done-for-you lines ([competitor analysis](./competitor-analysis.md)) |
| Prompt-to-app with hosting | Lovable, Replit, Bolt, Base44 | Different buyer; L4 offers a production-grade alternative for engineers |
| **Price per verified outcome; failed work free** | No self-serve product. Cognition has an enterprise-only guarantee, settled in credits at the end of an annual contract | **Differentiator (F5):** self-serve, per change, priced before work, refund on false green |
| **Holdout scenarios plus an evidence card on every change** | StrongDM internally; not productized for small teams | **Differentiator (F2, F4)** |
| **Agents structurally barred from production** | Varies: Factory's sandbox is opt-in and Missions need "High" autonomy; Amp demos granting production access | **Differentiator (F3):** safe by default, with a separate merge identity |
| **Lights-out earned per line from measured track records** | Not productized | **Differentiator (F4)** |

---

## 2. Product principles

1. **Value is a verified, merged change.** Code without evidence isn't a deliverable.
2. **Zero prompts to value.** The factory proposes, from the Repo X-ray and the issue tracker; the owner decides.
3. **Show evidence, not diffs.** The diff is one click away. The evidence card comes first.
4. **Risk decides the interruption:** Low, Medium or High by path and change type.
5. **Safe by construction.** Capabilities come from the sandbox, not from prompts.
6. **Honest by default.** Show failures, never charge for them, never call a change green that isn't.
7. **Autonomy is earned with evidence,** per line and per repository.
8. **Model-neutral.** Use the best agent for each station, measured. This is an expected feature now, not a differentiator.
9. **Respect the owner's time:** batches, one weekly report, no notification spam.
10. **No lock-in.** Normal Git, normal CI, an exportable Product Brain. Leaving is one click.

---

## 3. The seven bets in detail

### F1. Zero-prompt start: Repo X-ray plus Product Brain

**Problem:** blank chat boxes, agents that don't know the codebase, and setup that takes days.

**What we build:**
- **GitHub App install** → choose repositories → **Repo X-ray**, read-only, finishing in ≤ 10 minutes at p90. It reports:
  - test coverage gaps and flaky tests;
  - vulnerable and outdated dependencies;
  - missing CI or preview environments;
  - open bugs that are likely reproducible;
  - risky paths (auth, billing, migrations).
- **Five suggested orders**, each with a price and a risk tier. Approve one, and the first merged change arrives in ≤ 30 minutes.
- **Product Brain v1**, editable in a "What the factory knows" page:
  - architecture map, commands (build, test, run), conventions;
  - domain glossary, risky paths, decisions.
  
  It is built from the repository, docs and the first orders.

**Target to prove:** ≥ 60% of trials merge a verified change within 30 minutes of connecting.

**Paperclip reuse:** projects, project workspaces and repositories; company skills and documents; memory connectors; routines.

### F2. Verified changes

**Problem:** "almost right" code, test gaming, security flaws, review burden.

**What we build:**
- **Order contract:** an executable definition of done ([harness §4.1](./reliability-cost-harness.md#41-order-contract-schema-sketch)).
- **Checker library, L1–L3 and L7:** build, type, lint, tests (new tests fail first), SAST, dependency audit, secret and license scans, diff policy.
- **Holdout scenarios (L4):** written at spec time, hidden from the builder, run on the preview.
- **Twin services (L5):** fakes of Stripe, auth, email and storage, so integration paths are tested without credentials (GA).
- **Review agents (L6):** correctness and security, posted as GitHub reviews.
- **False-green audit:** a 7-day post-merge watch. Any false green blocks the line's lights-out status and opens an eval case.

**Target to prove:** first-pass merge rate ≥ 60% at beta and ≥ 75% at GA; false green = 0.

**Paperclip reuse:** `completion_contracts`, `work_assessments`, GitHub review checks, evals.

### F3. Safe by construction

**Problem:** agents running with developer credentials; the PocketOS-style deletion; injection through issues and dependencies.

**What we build:**
- Factory sandbox images with no mounted secrets and an egress allowlist.
- A merge service with its own identity. Agents can't merge to protected branches.
- A destructive-command filter.
- Diff policy for CI, test configuration, lockfiles and migrations.
- The low-trust preset applied to untrusted input.
- **A "Safety" page** listing exactly what agents can and cannot do, for customers' security questionnaires.

**Target to prove:** zero production-credential exposures; 100% of High-tier changes approved by a human; red-team suite passing before each release.

**Paperclip reuse:** sandbox providers, execution allowlist, managed GitHub launchers, low-trust containment, run secret redaction, tool-access policy.

### F4. Decisions, not code reviews

**Problem:** reading everything doesn't scale; reading nothing isn't safe.

**What we build:**
- **Evidence inbox,** grouped by tier:
  - **Low:** auto-merge once trusted;
  - **Medium:** batch approval;
  - **High:** individual approval.
- **Each card shows:** the order, the checks (✓ or ✗), holdout results, scan summary, preview link, cost, attempts and the model route. The diff is one click away.
- **Actions:** approve; request change (by text or voice); reject with a reason. A rejection becomes an eval case.
- **Lights-out ladder per line and repository** ([factory lines §6](./factory-lines.md#6-risk-tiers-and-the-lights-out-ladder-common-to-all-lines)): promotion is suggested with its evidence, and a revert demotes the line automatically.
- **Approve from the GitHub PR,** the Slack message or the inbox.

**Target to prove:** median decision ≤ 60 seconds per Medium change; ≥ 30% of Low-tier changes lights-out by GA for active accounts.

**Paperclip reuse:** approvals, decision queues, `decision_training_examples`, issue review policy.

### F5. Predictable economics and real humans

**Problem:** two-thirds of negative reviews are about money; 39% are about support; 24% say they paid for failure.

**What we build:**
- **A price quoted before work starts** (Small $3, Medium $12).
- **Charged only on merge.** "Couldn't finish" is free.
- **A hard monthly cap** you set.
- **Cost per change** on every card.
- **Bring-your-own-key mode** with zero markup.
- **A billing center:** cancel in ≤ 2 clicks, pause up to 3 months, a reminder 3 days before every charge, prices locked for 12 months after any change.
- **Human support promise:** ≤ 1 business hour (Team and Agency), ≤ 4 hours (Solo); a status page and incident notices within 30 minutes.

**Target to prove:** zero billing tickets unresolved after 48 hours; zero surprise charges; ≥ 90% of support first responses within the promise.

**Paperclip reuse:** budget policies and incidents, cost events, quota windows.

### F6. Operate what you ship

**Problem:** coding tools stop at the PR; instability shows up after merge.

**What we build:**
- **Beta:** preview environments (Vercel first; Railway and Fly next).
- **GA:**
  - feature flags and staged rollout;
  - automatic rollback on failed health checks;
  - error-tracker intake (Sentry first), so a regression becomes an L2 order automatically.

**Target to prove:** change-failure rate ≤ 15% at beta and ≤ 10% at GA; time to restore ≤ 1 hour for factory releases.

**Paperclip reuse:** Vercel connect, Railway services, workspace runtime services, routines.

### F7. The weekly factory report

**What it contains:**
- what shipped;
- the four DORA metrics, before and after the factory;
- cost per change against a human estimate;
- lights-out share;
- **what failed and why** (couldn't-finish reasons, reverts, false-green audit);
- next week's suggested orders.

**Shareable, with redaction.** This becomes the public "Factory Report" used in build-in-public.

**Target to prove:** ≥ 60% weekly open rate. Accounts that open it have week-8 retention ≥ 1.5x accounts that don't.

### Supporting capabilities (must match competitors; not differentiators)

- GitHub at beta; GitLab at GA.
- Linear, Jira and GitHub Issues as intake.
- Slack notifications and approvals.
- Model choice per station.
- Web app plus PWA.
- CLI to send an order from the terminal (`factory order "…"`).
- Export of all data.

---

## 4. The 10–100x scorecard (targets to prove, not claims to publish)

| Outcome | Today (baseline) | Target | Multiple | Evidence or method |
|---|---|---|---|---|
| Cost of a Medium change | ≈ $250–340 for a human (BLS median wage plus overhead, 3–4 h) | $12 price (≈ $5 cost) | **≈ 20–30x cheaper** | [Harness §6.3](./reliability-cost-harness.md#63-cost-per-change-assumptions-stated) |
| Reproducible bug → verified fix PR | Hours to days (measure in Phase 0) | ≤ 1 h | **10–50x** (to prove) | Phase 0 measurement |
| Security patch latency | Days to weeks (measure in Phase 0) | ≤ 24 h from advisory | **≈ 10–30x** (to prove) | Phase 0 measurement |
| Review time per Medium change | Reading the full diff (measure in Phase 0) | ≤ 60 s on the evidence card | **≈ 5–15x** (to prove) | Phase 0 measurement |
| Time to first merged change on a new repository | Days of agent setup | ≤ 30 min | **≈ 50x** | Onboarding funnel |
| Paying for failed work | Common under credits and compute units (24% of negative reviews) | $0 | — | VOC |
| Production credentials exposed to agents | Common (developer credentials) | 0 | — | Safety audit |
| Human support first response | Often none (39% of negative reviews) | ≤ 1 business hour | **10x+** | VOC |
| Engineering throughput per person | 1x | 2–5x merged, verified changes per week | **2–5x** (honest; not 10x overall at first) | Phase 0 and beta data |

**Rule:**
- We publish a multiple in marketing only after pilot data proves it for that line (FTC substantiation; [marketing plan §2.3](./marketing-plan.md#23-language-rules-brand-legal-and-trust)).
- Overall throughput gains at launch are about 2–5x. The 10–100x gains are on specific jobs (cost per change, patch latency, setup), and we say so.

---

## 5. What the customer sees

**Five tabs:**
- **Today:** the evidence inbox (by tier), orders in progress, a morning summary.
- **Orders:** a board by line and state (spec → plan → build → verify → review → release), with price and cost per order.
- **Releases:** what shipped, preview links, flags and rollouts, rollbacks.
- **Quality:** line track records (first-pass merge, false green, change-failure, lights-out status), the Repo X-ray, the DORA trend.
- **Cost & Report:** spend against the cap, cost per change, the weekly factory report.

**Settings:**
- Product Brain ("What the factory knows");
- Lines;
- Risk & trust (tiers, path rules, lights-out ladder);
- Repositories & connections;
- Plan & billing;
- Safety;
- Help (talk to a human);
- **Advanced:** agents, adapters, routines, models. These are hidden by default, consistent with Paperclip's rule of keeping developer internals out of the main path.

**Three flows that must be perfect:**
1. **The first 30 minutes:**
   1. Sign in with GitHub.
   2. Install the app on 1–3 repositories.
   3. The X-ray runs (≤ 10 min) while the owner answers 3 questions (stack, deploy target, risky paths).
   4. Five suggested orders appear, each with a price.
   5. Approve one.
   6. Watch it run on a live timeline.
   7. The evidence card arrives.
   8. Merge.
   9. A preview of the weekly report.
2. **The daily five minutes:**
   1. A morning summary: "6 changes ready: 4 Low (auto-merged), 2 Medium (batch), 0 High."
   2. Approve the batch.
   3. Done.
3. **The Friday ten minutes:**
   1. The weekly factory report.
   2. "What didn't work."
   3. Approve next week's suggested orders and maintenance plan.

---

## 6. Prioritized backlog (RICE)

**Scoring:**
- **Reach:** share of target accounts affected (0–10).
- **Impact:** 0.5 low · 1 medium · 2 high · 3 massive.
- **Confidence:** strength of evidence.
- **Effort:** person-weeks on the Paperclip fork.
- **Score** = Reach × Impact × Confidence ÷ Effort.

All scores are estimates to revisit with Phase 0 data.

| Rank | ID | Feature | Bet | Reach | Impact | Conf. | Effort (pw) | Score | Phase |
|---|---|---|---|---|---|---|---|---|---|
| 1 | S5 | Merge service with risk-tier policy and branch-protection checks | F3/F4 | 10 | 3 | 90% | 3 | **9.0** | Beta |
| 2 | S18 | False-green audit and 7-day post-merge watch | F2 | 10 | 2 | 80% | 2 | **8.0** | Beta |
| 3 | S1 | Outcome-priced usage ledger and billing center (quote, charge on merge, cap, cancel, pause) | F5 | 10 | 3 | 80% | 4 | **6.0** | Beta |
| 4 | S8 | Bug line (L2) package and evals | Lines | 9 | 3 | 80% | 4 | **5.4** | Beta |
| 5 | S11 | Human support promise, status page, incident notices | F5 | 10 | 2 | 80% | 3 | **5.3** | Beta |
| 6 | S10 | Weekly factory report with DORA metrics | F7 | 10 | 2 | 80% | 3 | **5.3** | Beta |
| 7 | S16 | Onboarding: GitHub App install, plans, trial | F1 | 10 | 2 | 80% | 3 | **5.3** | Beta |
| 8 | S6 | Repo X-ray with five suggested orders | F1 | 10 | 3 | 70% | 4 | **5.2** | Beta |
| 9 | S3 | Code checker library (L1–L3, L7) and order-contract extensions | F2 | 10 | 3 | 80% | 5 | **4.8** | Beta |
| 10 | S2 | Evidence card and evidence inbox (tiers, batch approval) | F4 | 10 | 3 | 80% | 5 | **4.8** | Beta |
| 11 | S12 | Order sizing, routing, cache telemetry, escalation on retry | F2/F5 | 10 | 2 | 70% | 3 | **4.7** | Beta |
| 12 | S19 | Export, deletion and data controls | F5 | 10 | 1 | 90% | 2 | **4.5** | Beta |
| 13 | S4 | Factory sandbox images (TypeScript, Python), egress policy, no secrets | F3 | 10 | 3 | 70% | 5 | **4.2** | Beta |
| 14 | S13 | Holdout-scenario runner on previews (basic) | F2 | 7 | 3 | 60% | 3 | **4.2** | Beta |
| 15 | S24 | Lights-out ladder with sampling | F4 | 8 | 2 | 70% | 3 | **3.7** | GA |
| 16 | S9 | Maintenance line (L3) package and evals | Lines | 9 | 2 | 80% | 4 | **3.6** | Beta |
| 17 | S17 | Feature line (L1) preview package | Lines | 8 | 3 | 60% | 4 | **3.6** | Beta |
| 18 | S7 | Product Brain v1 | F1 | 10 | 2 | 70% | 4 | **3.5** | Beta |
| 19 | S14 | Preview environments adapter (Vercel first) | F6 | 7 | 2 | 70% | 3 | **3.3** | Beta |
| 20 | S27 | Error-tracker intake (Sentry first) → L2 orders | F6 | 7 | 2 | 70% | 3 | **3.3** | GA |
| 21 | S20 | Feature line GA (full holdouts, flags, staged rollout) | Lines/F6 | 9 | 3 | 60% | 5 | **3.2** | GA |
| 22 | S15 | Factory UI shell (Today, Orders, Releases, Quality, Cost) on Paperclip's UI | UX | 10 | 2 | 80% | 5 | **3.2** | Beta |
| 23 | S23 | Team plan: seats, review routing, SSO-lite | Parity | 6 | 2 | 80% | 4 | **2.4** | GA |
| 24 | S26 | Release and rollback adapters (flags; Vercel, Railway, Fly) | F6 | 7 | 2 | 60% | 4 | **2.1** | GA |
| 25 | S22 | Agency line (L5): client workspaces, per-client reports, handover packs | Lines | 4 | 3 | 70% | 5 | **1.7** | GA |
| 26 | S29 | Public factory benchmark harness | Marketing | 10 | 1 | 60% | 4 | **1.5** | GA |
| 27 | S25 | Twin services (Stripe, auth, email, storage) | F2/F3 | 6 | 2 | 60% | 5 | **1.4** | GA |
| 28 | S28 | GitLab support | Parity | 3 | 2 | 80% | 4 | **1.2** | GA |
| 29 | S21 | Greenfield SaaS line (L4) blueprint | Lines | 4 | 2 | 60% | 6 | **0.8** | GA |
| — | S30 | Legacy modernization line | Expansion | — | — | — | 10+ | — | Later |
| — | S31 | Mobile line (Expo) | Lines | — | — | — | 6 | — | Later |
| — | S32 | Community line registry | Community | — | — | — | 4 | — | Later |
| — | S33 | SAML SSO, audit export (mid-market) | Expansion | — | — | — | 4 | — | Later |
| — | S34 | Local-runner mode, generally available | F5 | — | — | — | 4 | — | Later |
| — | S35 | EU data residency | Expansion | — | — | — | 6 | — | Later |
| — | S36 | "OPC operations" layer (the parked front office, revenue and content features) | Expansion | — | — | — | 20+ | — | Later |

**Totals:**
- **Beta:** S1–S19 = **69 person-weeks** of engineering. Adding design (≈ 6) and security and QA (≈ 5) gives ≈ 80.
- **GA:** S20–S29 ≈ **43 person-weeks.**

**Reading the ranking:**
- **Cheap trust and safety features score highest:** merge policy, false-green audit, billing, support. They are also the marketing proof.
- **The biggest differentiators have lower RICE scores because of effort,** not value: the checker library, the evidence inbox, sandboxes, the X-ray. They stay in beta regardless.
- **If the team is smaller than about 6 builders,** cut S17 (L1 preview) and S13 (holdouts) to W+4. Beta then ships L2 and L3 only (≈ 62 pw).

---

## 7. Roadmap

| Window | Build | Lines | Exit criteria |
|---|---|---|---|
| **Phase 0** (October to mid-November 2026) | Concierge factory on the Paperclip fork; S3, S4, S5 prototypes | L2, L3 (hand-operated where needed) | Go/no-go gates in [market research §8](./market-research.md#phase-0-validate-october-to-mid-november-2026-46-weeks) |
| **Build to beta** (mid-November 2026 to January 2027) | S1–S19 | L2, L3 GA-in-beta; L1 preview | First-pass merge rate ≥ 60%; false green = 0; Medium cost ≤ $6 p50; billing end-to-end tests pass |
| **Public beta** (W0 = week of 25 Jan 2027) | Launch; founding pricing | Same | ≥ 50% of trials merge a change within 30 minutes; week-4 retention ≥ 35% |
| **GA** (late April 2027) | S20–S29 | + L1 GA, L4, L5 | First-pass merge rate ≥ 75%; change-failure rate ≤ 10%; week-4 retention ≥ 45%; SOC 2 Type I |
| **Later** (May 2027 onward) | S30–S36 | + L6 API, L7 Mobile; legacy modernization | Mid-market pilots; benchmark published quarterly |

**Build vs integrate:**

| Area | Decision |
|---|---|
| Coding agents | **Integrate** through Paperclip adapters (Claude Code, Codex, Cursor, Gemini, OpenCode and others). Never build our own model or IDE |
| Code hosting and CI | **Integrate** with GitHub (beta) and GitLab (GA), using the customer's existing CI. No hosted CI of our own at beta |
| Sandboxes | **Buy** (E2B, Daytona, Modal via Paperclip providers); our own images |
| Previews and deploys | **Integrate** with Vercel, Railway and Fly. No hosting of customer apps |
| Error tracking and monitoring | **Integrate** with Sentry first; Datadog later |
| Security scanning | **Integrate** open-source scanners (Semgrep OSS, OSV-Scanner, Gitleaks or similar) inside sandboxes; optional Snyk integration |
| Billing | **Buy** Stripe Billing plus Stripe Tax |
| Support and status | **Buy** Plain or Intercom; Instatus |

---

## 8. Build on Paperclip: reuse map

| Need | Paperclip today | Extend with |
|---|---|---|
| Orders and breakdown | Issues, sub-issues, blockers, `issue_plan_decompositions` | Order sizes, price quotes, line templates |
| Agents and models | 12 adapters, AI connection defaults, quota windows | Per-station routing; cost per merged change |
| Execution | Execution workspaces, 8 sandbox providers, runtime leases, execution allowlist | Factory images, egress presets, twin services |
| GitHub | Managed launchers, review checks, PR reviews, merge-state resolver | Merge service and risk-tier policy |
| Definition of done | `completion_contracts`, `work_assessments`, native completion reviews | Code checker library, holdout runner, evidence card |
| Decisions | Approvals, decision queues, issue review policy, `decision_training_examples` | Evidence inbox, batch approval, lights-out ladder |
| Safety | Low-trust containment, run secret redaction, tool-access policy | Destructive-command filter; Safety page |
| Cost | Budget policies and incidents, cost events | Outcome-priced usage ledger; per-order caps |
| Recurring work | Routines, task watchdog | Maintenance schedules |
| Deploy | Vercel connect, Railway services | Previews, flags, rollback |
| Evals | Runner and product end-to-end evals | Per-line golden sets; public benchmark |
| Teams and templates | Teams catalog (includes a software-development team), company import and export | Line packages in the same format |
| Chat | Slack, Discord, Teams, Telegram, GitHub chat surfaces | Slack approvals for evidence cards |

**Net-new builds:**
- the outcome-priced billing center;
- the support console and status page;
- the Repo X-ray;
- the holdout-scenario runner;
- twin services;
- the factory UI shell;
- the public benchmark.

---

## 9. What we will not build, and why

| Anti-feature | Why not |
|---|---|
| "Replace your engineers" autopilot (Level 5 by default) | Delegation is 0–20% today; trust is falling. Autonomy is earned per line (F4) |
| Agents with production credentials or cloud-admin access | PocketOS; the lethal trifecta. Releases go only through the customer's pipeline |
| Credits, compute units or opaque usage meters | 49% of negative reviews cite credits and usage; we price per merged change |
| A new IDE or editor | Labs and Cursor own this; we integrate with whatever developers use |
| Our own frontier model | Model-neutral routing is expected by customers; labs improve faster than we could |
| A no-code app builder for non-engineers | A different buyer with the worst VOC economics; served through agencies (L5) instead |
| A general chat assistant | Bundled free by every platform |
| Hosting customer apps | Vercel, Railway and Fly exist; hosting creates lock-in and liability |
| Skipping or deleting tests to get green | Never. It is enforced by diff policy and holdout scenarios |

---

## 10. Validation plan (Phase 0 → beta)

| Bet | Experiment | Success | Kill or rethink if |
|---|---|---|---|
| F1 X-ray and Brain | Run the X-ray on 12 partner repositories; partners rate the five suggested orders | ≥ 3 of 5 suggestions accepted on average | < 2 accepted; the X-ray can't run the test suite on ≥ 30% of repositories |
| F2 Verified changes | 4 weeks of L2 and L3 orders with full checks | First-pass merge ≥ 50%; false green = 0 | False green > 0 twice; first-pass merge < 40% |
| F3 Safety | Red-team exercise on sandbox images and injection suite | 0 escapes; 0 secret exposures | Any production-credential exposure |
| F4 Evidence inbox | Time decisions with and without evidence cards (A/B within partners) | Median ≤ 60 s for Medium; partners prefer cards | Partners still read full diffs for > 70% of Medium changes |
| F5 Pricing | Paid pilot at Small $3 / Medium $12; Van Westendorp survey; offer bring-your-own key | ≥ 6 of 12 pay; ≤ 30% choose bring-your-own key | < 4 of 12 pay at any tested price |
| F6 Operate | Previews on Vercel-hosted partner apps | Preview health checks work for ≥ 80% of those apps | — |
| F7 Report | Weekly report sent to all partners | ≥ 60% open; at least one "this changed my week" quote | < 30% open |

**Overall go/no-go:**
- ≥ 40% of partners would be "very disappointed" without the factory (Sean Ellis test);
- Medium cost ≤ $6 at p50.

---

## 11. Risks

| Risk | Mitigation |
|---|---|
| Labs ship a "factory" mode with verification | Stay model-neutral; win on outcome pricing, small-team UX, evidence and human support; integrate their agents |
| Reliability is lower on messy small-team codebases | L2 and L3 first; order sizing; the X-ray identifies repositories that aren't ready ("add tests first" orders) |
| Holdout scenarios are too costly for owners to write | The factory drafts them from the spec; owners only approve; start with 3 per feature |
| Outcome pricing invites gaming (splitting work to cut price) | Size is set by the planner, not the customer; price shown before approval |
| Upstream Paperclip changes break the fork | Thin fork, upstream contributions, module boundaries, weekly upstream merge |

## Sources

See the [market research v3 data sources](./market-research.md#data-sources) and the [harness sources](./reliability-cost-harness.md#sources). Key evidence:
- [DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/)
- [CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report)
- [Veracode 2026](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/)
- [Anthropic 2026 Agentic Coding Trends Report](https://resources.anthropic.com/2026-agentic-coding-trends-report)
- [Stack Overflow 2025](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/)
- [METR](https://metr.org/time-horizons/)
- [VKTR on Claude Code Review](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/)
- [CSA research note](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/)

## Method notes

- **Voice-of-customer coding** used keyword rules with overlapping themes, plus a manual spot-check. Trustpilot skews toward app-builder users; Hacker News skews toward experienced engineers. Reddit blocked automated access, so Phase 0 interviews cover that gap.
- **RICE efforts** assume a Paperclip fork and a team of about 7 builders. Re-estimate after Phase 0.
- **Scorecard baselines** marked "measure in Phase 0" have no reliable public number. We won't publish multiples for them until measured.
