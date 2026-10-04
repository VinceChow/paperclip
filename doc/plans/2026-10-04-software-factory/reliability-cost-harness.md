# The Factory Harness: Reliability, Safety and Cost

**Date:** 2026-10-04 (v2; replaces the [OPC outcome-loop harness](../2026-09-26-opc-platform/reliability-cost-harness.md))
**Part of:** [Market research v3](./market-research.md) · [Factory lines](./factory-lines.md) · [Product feature strategy](./product-feature-strategy.md) · [PRD v2](./prd.md) · [Marketing plan](./marketing-plan.md)
**Question:** How does the factory make sure every change it ships is correct, safe and affordable? What harness and loop engineering does that need, and how much of it does Paperclip already have?

---

## 1. Summary

**Coding agents fail in known ways:**
- they produce "almost right" code (about 1.7x more issues per PR);
- they introduce security flaws (a 56% security pass rate);
- they declare work done too early;
- they game tests (METR measured reward hacking in 30% of runs on one task suite);
- they take destructive actions with credentials they shouldn't have.

A better model reduces these problems but doesn't remove them. **The harness is the product.**

**The design is a factory loop.**
- **Small orders:** every change is split into an order sized to what agents finish reliably on this repository.
- **Executable definition of done:** each order carries one, made of tests written before the code, holdout scenarios stored outside the repository, scans and preview health.
- **Separate roles:** a doer builds; separate checkers verify.
- **Risk tiers** decide when a human looks.
- **Sandboxes only:** nothing touches production except through the customer's own release pipeline.
- **Learning:** every revert, edit or rejection becomes an eval case.

**Cost works with routing, caching and order sizing.**
- A Medium change (1–3 hours of human work) costs about **$5** in models and sandbox.
- The same work costs about **$8** if run entirely on Opus 5.5, about **$15** without caching, and about **$18** entirely on Fable 5.1.
- An "always-on agent team" design (5 agents on 30-minute heartbeats) adds about **$980 a month** per account, whatever it produces.

**Paperclip already has most of the control plane.** Present today:
- 12 agent adapters and 8 sandbox providers;
- execution workspaces;
- managed GitHub identity, GitHub review checks and PR merge state;
- low-trust containment and secret redaction;
- approvals, budgets, native completion contracts and work assessments;
- routines, the watchdog and evals.

Still to build:
- the **code checker library** and holdout-scenario runner;
- **order sizing**;
- the **evidence card and inbox**;
- **twin services**;
- release and rollback adapters;
- the **outcome-priced usage ledger**.

## 2. Why coding agents don't finish jobs correctly (evidence)

| Failure | Evidence | Harness response |
|---|---|---|
| "Almost right" changes | 10.83 vs 6.45 issues per PR (about 1.7x); logic issues +75% ([CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report)). The top developer complaint, at 66%, is "almost right" ([Stack Overflow 2025](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/)) | Tests before code; holdout scenarios; review agents; diff-size limits |
| Insecure code | Security pass rate flat at 56% across 100+ models ([Veracode 2026](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/)) | SAST, dependency and secret scans as required checks; a security review agent; secure blueprints |
| Premature completion and overambition | Agents leave features half-implemented and mark them complete without testing ([Anthropic, long-running harnesses](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)) | One order at a time; every criterion starts as "failing"; an independent verifier |
| Reward hacking (gaming tests) | 30.4% of runs on RE-Bench tasks; warnings barely help (80% → 70% on one task) ([METR](https://metr.org/blog/2025-06-05-recent-reward-hacking/)) | **Holdout scenarios the builder never sees.** Test files are locked after the "tests first" step. Diffs that touch test or CI files are tier-raised and flagged |
| Instability at the team level | AI raises throughput and change-failure rates; it amplifies existing practice ([DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/)) | The factory supplies the missing practice: tests, CI, preview, flags, rollback |
| Tasks too long for current agents | Reliable (80%) horizon of about 3.1 h for the best measured model; 17.4 h at 50% ([METR](https://metr.org/time-horizons/)) | Order sizing per repository (§4.3) |
| Destructive actions | A production database and its backups deleted in 9 seconds via an unrelated over-privileged token ([PocketOS](https://www.tomshardware.com/tech-industry/artificial-intelligence/claude-powered-ai-coding-agent-deletes-entire-company-database-in-9-seconds-backups-zapped-after-cursor-tool-powered-by-anthropics-claude-goes-rogue)) | **Safe by construction** (§4.6): no production credentials; destructive-action gate; sandbox egress rules |
| Prompt injection through issues, dependencies and web content | The "lethal trifecta": private data + untrusted content + the ability to communicate externally ([Simon Willison](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/)) | Never combine all three in one step. Low-trust preset for untrusted input; egress allowlists; no secrets in build sandboxes |
| Large, unfamiliar codebases | 17% of first-person Hacker News comments on coding agents discuss context and large codebases ([market research §3.4](./market-research.md#34-what-they-struggle-with-today-two-voice-of-customer-sources)) | Product Brain (architecture map, conventions); Repo X-ray; scoped context per order |
| Review becomes the bottleneck | Output per Anthropic engineer up about 200%; review became the constraint ([VKTR](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/)); review burden is the top Hacker News theme (24%) | An evidence card instead of raw diffs; batch approval; risk tiers; lights-out per line |

## 3. Design principles

1. **Orders, not open-ended sessions.** Each order has one purpose, one definition of done, one budget and one evidence card.
2. **Size work to measured reliability.** Order size follows the repository's own pass rates, and grows only as the evidence grows.
3. **Tests and scenarios before code.** The builder must first write checks that fail. Holdout scenarios stay hidden from the builder.
4. **Separate the doer from the checkers.** Verification runs in a fresh context with different instructions, and for review agents, often a different model.
5. **Deterministic checks first.** Compilers, type checkers, tests, linters and scanners run before any model judgment. They are fast, cheap and objective ([Anthropic, evals](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)).
6. **Safe by construction, not by instruction.**
   - Agents have no production credentials and no destructive tools.
   - Network egress is limited.
   - A prompt can't grant a capability the sandbox doesn't have.
7. **Risk decides the interruption.** Low, Medium and High tiers by path and change type. High is never automatic in v1.
8. **Event-driven, not timer-driven.** Wake on issues, error events, advisories and spec approvals. Use low-frequency schedules only for maintenance and reports.
9. **Cost is a service-level objective.** Measure cost per *merged* change (p50 and p90), cap every order, and make failed orders free to the customer. That gives us the incentive to fail cheaply.
10. **Honest failure beats fake green.** "Couldn't reproduce" and "couldn't finish" are first-class outcomes with evidence of what was tried. *False green* is the worst defect we can ship, and it is a release blocker.
11. **Learn from every correction.** Reviewer edits, rejections, reverts and incidents become eval cases. Capability and regression suites stay separate.
12. **Model-neutral.** Route each station to the best model or agent for the job, measured per line. Never depend on one provider's agent.

## 4. The factory loop

```
 intake (issue / error event / advisory / spec / schedule)
        │
        ▼
 ┌──────────────┐  Product Brain + Repo X-ray context; missing info? ──► ask owner (one question, options)
 │  SPEC        │  acceptance checks + holdout scenarios (stored outside the repo)
 └──────┬───────┘  High-impact specs need owner approval
        ▼
 ┌──────────────┐  split into orders sized to this repo's measured pass rate;
 │  PLAN        │  dependencies; price quoted per order before work starts
 └──────┬───────┘
        ▼
 ┌──────────────┐  sandbox (no prod creds, egress allowlist); tests-first step,
 │  BUILD       │  then code; routed model; cached prefix          ◄──────────┐
 └──────┬───────┘                                                            │ revise (≤ 2)
        ▼                                                                    │ escalate model
 ┌──────────────┐  L1 compile/type/lint · L2 tests (new + suite) · L3 scans  │ once
 │  VERIFY      │  L4 holdout scenarios on preview · L5 twin services        │
 │              │  L6 review agents (correctness, security) · L7 diff policy ├─ fail
 └──────┬───────┘                                                            │
        │ pass                     budget/attempts exhausted ──► "couldn't finish" + evidence (free)
        ▼
 ┌──────────────┐  evidence card; risk tier decides: auto (trusted Low) /
 │  REVIEW      │  batch (Medium) / individual (High)  ── edit/reject ──► eval case ──► BUILD
 └──────┬───────┘
        ▼
 ┌──────────────┐  merge via the customer's protected branch + CI; feature flag;
 │  RELEASE     │  staged rollout; automatic rollback on health-check failure
 └──────┬───────┘
        ▼
 ┌──────────────┐  post-merge CI on main, health checks, error-rate watch (7 days)
 │  OPERATE     │  regression or incident ──► new L2 order; mark the original "false green" if it caused it
 └──────┬───────┘
        ▼
 ┌──────────────┐  weekly factory report; line track records; eval growth
 │  LEARN       │
 └──────────────┘
```

### 4.1 Order contract (schema sketch)

This extends Paperclip's native `completion_contracts` (which already record per-issue criteria, risk and completion authority) with executable code checks.

```yaml
order:
  line: feature
  title: "Add CSV export to invoices page"
  size: medium                       # small | medium (large is split by the planner)
  price_usd: 12                      # quoted before work starts; charged only if merged
  budget: { usd_hard_cap: 10, max_attempts: 3, max_revisions: 2, wall_clock_min: 90 }
  risk_tier: medium                  # raised automatically by path rules (auth, billing, migrations…)
  definition_of_done:                # every criterion starts "failing"
    - { id: tests_first,      check: code,     rule: "new tests fail on base commit" }
    - { id: suite_green,      check: code,     rule: "full test suite passes" }
    - { id: types_lint,       check: code,     rule: "typecheck and lint clean" }
    - { id: scans_clean,      check: code,     rule: "no new high/critical SAST, dependency or secret findings" }
    - { id: holdout,          check: scenario, rule: "3/3 holdout scenarios pass on preview", hidden_from_builder: true }
    - { id: preview_healthy,  check: external, rule: "preview deploy healthy; no console errors on scenario pages" }
    - { id: review_ok,        check: agents,   rule: "correctness + security reviewers: no blocking findings" }
    - { id: diff_policy,      check: code,     rule: "<= 400 changed lines; no edits to CI, test config or lockfile unless declared" }
  evidence_card: [checks, scenario_results, scan_summary, preview_url, cost_usd, attempts, model_route]
  on_fail: report_with_evidence      # never mark done; customer not charged
```

### 4.2 Verification tiers for code

| Tier | Check | Cost | Required for |
|---|---|---|---|
| **L1** | Build, typecheck, lint, format | Cents | All orders |
| **L2** | Tests: new tests fail first, then pass; full suite green; mutation check on changed lines (Maintenance coverage jobs) | Cents–dimes | All orders |
| **L3** | SAST, dependency audit, secret scan, license scan | Cents | All orders |
| **L4** | **Holdout scenarios** (end-to-end user stories stored outside the repository, run against the preview environment) | Dimes | Feature, Greenfield, Agency lines; bug fixes with a user-visible symptom |
| **L5** | **Twin services** (local fakes of Stripe, auth providers, email and similar external APIs) for integration paths | Dimes | Orders that touch external integrations |
| **L6** | Review agents: correctness and security; style only when a convention is written in the Product Brain | $0.50–1 | Medium and High orders |
| **L7** | Diff policy: size limits; protected files (CI, test configuration, lockfiles, migrations) | Free | All orders |
| **Post-merge** | CI on `main`, health checks, error-rate watch for 7 days; false-green audit | Cents | All merged changes |

### 4.3 Order sizing (from METR's horizon data to each repository)

- **Starting point.** METR's best measured agent completes about **3.1 hours** of expert work 80% of the time ([METR](https://metr.org/time-horizons/)). Real repositories are messier than benchmark tasks, so the planner starts each new repository at **Small (≤ 30 min) and Medium (1–3 h)** orders.
- **Measurement.** For each repository and line, the factory tracks first-pass merge rate and false-green rate by order size.
- **Growth.** It raises the size ceiling only when the first-pass merge rate at the current ceiling is ≥ 75% over the last 20 orders and the false-green rate is 0. It lowers the ceiling after two consecutive failures at that size.
- **Pace.** METR's fitted doubling time is about 129 days. If that holds, the reliable size grows about 7x a year, and the planner picks that up automatically without a redesign.

### 4.4 Retry and escalation

1. **First attempt** on the routed model at medium effort.
2. **On a check failure,** revise using the failed criteria as feedback (up to 2 revisions).
3. **On a second failure,** escalate the effort or model tier once. Anthropic measured "re-run failures at higher effort" at about 97% pass for about 45% lower cost than running everything at high effort ([Anthropic cost guidance](https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence.md)).
4. **Cap at 3 attempts,** consistent with Paperclip's three-attempt recovery budget. Then end as "couldn't finish," with evidence. The order is free to the customer.
5. **The watchdog** restarts orders that stopped for the wrong reason ([`doc/TASK-WATCHDOG.md`](../../TASK-WATCHDOG.md)).

### 4.5 Holdout scenarios and twin services

- **Holdout scenarios** are written at the spec step, approved with the spec, and stored in the factory, not in the repository. Each is an end-to-end user story in Given/When/Then form, plus a scripted browser or API check. The builder never sees them; the verifier runs them against the preview. This is StrongDM's answer to reward hacking, adapted for small teams ([Simon Willison](https://simonwillison.net/2026/Feb/7/software-factory/)).
- **Twin services** are lightweight fakes of common third-party APIs that run inside the sandbox:
  - Stripe, auth providers, email and object storage at beta;
  - more by line demand.
  
  Agents test integrations without real credentials or rate limits. Twins are shared across all customers and kept compatible with the official client libraries.

### 4.6 Safe by construction

| Capability | Agents in build and verify sandboxes | How it's enforced |
|---|---|---|
| Read and write the repository working copy | ✅ | Execution workspace per order |
| Push branches, open PRs, post reviews | ✅ (scoped to the order's branch) | Managed token-free `git`/`gh` launchers bound to the run's accepted identity ([doc](../../execution-github-identity.md)) |
| Merge to protected branches | ❌ (the factory's merge service does this after the risk-tier decision) | Branch protection plus a separate merge identity |
| Production credentials, cloud admin tokens, database URLs | ❌ **Never** | Secrets are not mounted; secret scan on the workspace; run secret redaction |
| Network egress | Package registries, the git host, docs allowlist | Sandbox egress policy; low-trust preset for untrusted input ([doc](../../LOW-TRUST-PRESETS.md)) |
| Destructive commands (`rm -rf` outside the workspace, `DROP`, volume and branch deletion, force-push) | ❌ | Tool policy plus command filter; High tier plus a human for any declared destructive migration |
| Edit CI, test configuration, lockfiles, migrations | Only if declared in the order | Diff policy (L7) raises the tier |
| Run against twin services | ✅ | Twins in the sandbox image |

## 5. Measuring reliability

| Metric | Definition | Beta target | GA target |
|---|---|---|---|
| **First-pass merge rate** | Orders merged without reviewer edits ÷ orders presented | ≥ 60% | ≥ 75% |
| **False-green rate** | Merged changes with an all-green evidence card that, within 7 days, fail CI on `main`, are reverted, cause an incident or fail a holdout re-run | **0** | **0** |
| **pass^3 on golden tasks** | All 3 repeated runs pass the definition of done | ≥ 85% per line before release | Same |
| **Couldn't-finish rate** | Orders ending without a merge ÷ orders started | ≤ 30% | ≤ 20% |
| **Change-failure rate** | Merged changes causing a rollback, hotfix or incident | ≤ 15% | ≤ 10% |
| **Revert rate (lights-out lines)** | Reverts ÷ auto-merged changes | ≤ 2% | ≤ 1% |
| **Cost per merged change** | All model, sandbox and failed-attempt cost ÷ merged changes, per size | Medium ≤ $6 p50, ≤ $12 p90 | Medium ≤ $5 p50 |
| **Review time** | Median human decision time per Medium change | ≤ 60 s | ≤ 45 s |
| **Cycle time** | Order created → merged (Medium) | ≤ 4 h | ≤ 2 h |
| **Lights-out share** | Merged changes with no human decision ÷ all merged | Tracked | ≥ 30% of Low tier |

**The four DORA metrics** (deployment frequency, lead time, change-failure rate, time to restore) appear in every weekly factory report, before and after the factory, for each repository.

**Eval program:**
- 20–50 golden tasks per line from design-partner repositories, with holdout scenarios.
- Code graders first.
- Model reviewers calibrated against human labels (≥ 85% agreement).
- pass^3 on every line, model or prompt change. Deploys are blocked on regression.
- Capability suites are kept separate from regression suites.
- **Price the tail:** report cost p90, not just the average.

## 6. Cost engineering

### 6.1 Prices used (Claude API list, 2026-10-04)

| Model | Input / output per million tokens | Cache read | Use in the factory |
|---|---|---|---|
| Claude Haiku 4.5 | $1 / $5 | $0.10 | Triage, classification, log summarizing, simple checks |
| Claude Sonnet 5.5 | $2 / $10 | $0.20 | Build, fix, review agents, most stations |
| Claude Opus 5.5 | $4 / $20 | $0.20 (0.05x) | Planning, specs, hard revisions, escalation |
| Claude Fable 5.1 | $10 / $50 | $0.25 (0.025x) | Rare: hardest escalations only |

Other prices that matter:
- 5-minute cache writes are 1.25x input; 1-hour writes are 2x.
- Batch is 50% off (for X-ray refreshes, reports and evals).
- Sandboxes (E2B or Daytona list price): $0.0504 per vCPU-hour plus $0.0162 per GiB-hour, so a 2 vCPU / 4 GiB sandbox is about **$0.17 an hour** ([Northflank](https://northflank.com/blog/ai-sandbox-pricing)).
- Other agent adapters (Codex, Gemini and others) are routed by measured cost per *merged* change, not by list price.

Sources: [Claude API pricing](https://platform.claude.com/docs/en/about-claude/pricing).

### 6.2 Levers ranked (Anthropic's measured effects; re-measure on factory workloads)

| Lever | Measured effect | Apply in the factory |
|---|---|---|
| **Prompt caching** | 2.7–5.3x cheaper agent loops at 79–90% hit rates | Stable prefix: system → tools → Product Brain → line instructions; volatile diff and logs after the breakpoint; track `cache_read_input_tokens` |
| **Routing by cost per solved task** | A mid-tier model at medium effort often beats a frontier model at default effort on cost per solved task | Sonnet builds; Opus plans and escalations; Haiku triages. Measured per line |
| **Re-run failures at higher effort** | About 97% pass for about 45% less cost | §4.4 |
| **Order sizing** | Failed long tasks waste the most tokens | §4.3 |
| **Deterministic checks first** | Cents instead of dollars | §4.2 |
| **Batch API** | 50% off | X-ray refresh, weekly report, evals |
| **Narrow tools and context** | Cost stays flat as tool count grows when tools are searched, not loaded | Per-station tool lists; scoped retrieval from the Product Brain |
| **Don't under-cap output** | A 16K cap cut off 25–43% of agentic attempts | ≥ 64K for agentic runs, with streaming |

Source: [Anthropic, optimizing for cost and intelligence](https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence.md).

### 6.3 Cost per change (assumptions stated)

**Medium change (1–3 h of human work), routed and cached:**

| Station | Model | Tokens (input / output) | Cost |
|---|---|---|---|
| Plan | Opus 5.5 | 300K (80% cache reads) / 15K | $0.65 |
| Build (tests first, then code) | Sonnet 5.5 | 4.0M (90% cache reads) / 80K | $2.52 |
| Review agents (correctness, security) | Sonnet 5.5 | 1.0M (80% cache reads) / 20K | $0.86 |
| Sandbox, CI, scans, preview | — | About 0.9 sandbox-hours | $0.15 |
| Revision allowance (30% of orders revise once) | Sonnet 5.5 | — | $0.76 |
| **Total** | | | **≈ $4.94** |

- **Small change:** ≈ $1–2.
- **Failed orders:** about 25% of orders at beta, averaging about $3 each, which adds about **$1 per merged change**.

**Cross-check:** Anthropic's enterprise Claude Code average is about $13 per active developer-day ([docs](https://code.claude.com/docs/en/costs)). At 2–4 changes a day, that is about $3–6 per change.

| Same Medium change, different design | Cost |
|---|---|
| **Factory design** (routed, cached, sized) | **≈ $5** |
| Everything on Opus 5.5, cached | ≈ $8 |
| Routed but **no caching** | ≈ $15 |
| Everything on Fable 5.1, cached | ≈ $18 |
| Org chart of 5 always-on agents on 30-minute heartbeats | + ≈ **$980 a month** per account, regardless of output |

**Per-account monthly view (Managed mode; prices from [market research §6.3](./market-research.md#63-pricing-recommendation-decision-d5-to-validate-in-phase-0)):**

| Account | Merged Medium-equivalents | Model + sandbox cost (incl. failures, X-ray, report) | Revenue | Gross margin |
|---|---|---|---|---|
| Solo founder | 30 | ≈ $185 | $29 + 30 × $12 = $389 | ≈ 52% |
| Small team | 80 | ≈ $485 | $199 + 80 × $12 = $1,159 | ≈ 58% |
| Agency | 150 | ≈ $910 | $399 + 150 × $12 = $2,199 | ≈ 59% |

**Bring-your-own-key accounts** pay their provider directly. Our cost is the sandbox and platform, under $0.20 per change, against a $79–799 platform fee.

### 6.4 Budget enforcement (layers)

1. **Per order:** a hard dollar cap and wall-clock limit in the contract. A capped order ends as "couldn't finish," and the customer isn't charged.
2. **Per line per day:** concurrency and rate limits (for example, at most 10 Maintenance orders a day per repository at beta).
3. **Per account per month:** a customer-set hard cap. When it's reached, new orders queue for approval, and nothing is charged automatically beyond the cap. This is Paperclip's budget hard-stop invariant, applied.
4. **Platform:** an anomaly alert when an account's cost per change exceeds 2x the line's p90; provider-level spend limits as the final backstop.

## 7. Paperclip today: what exists vs what to build

| Capability needed | Exists in this repository | Gap for the factory |
|---|---|---|
| Orders and breakdown | ✅ Issues, sub-issues, blockers, `issue_plan_decompositions` ([execution semantics](../../execution-semantics.md)) | Order sizing from measured pass rates; price quote per order |
| Many agents, model-neutral | ✅ 12 adapters (`packages/adapters/`) | Per-station routing policy; cost-per-merged-change telemetry |
| Sandboxes | ✅ 8 providers (`packages/plugins/sandbox-providers/`: Cloudflare, CreateOS, Daytona, E2B, exe.dev, Kubernetes, Modal, Novita); execution workspaces; runtime leases; an execution allowlist that forces untrusted tenants into sandboxes | Factory sandbox images per line; egress policy presets; **twin services** |
| GitHub | ✅ Managed launchers bound to the run's identity; GitHub review checks and PR reviews (`chat-github-checks`, `chat-github-reviews`); PR merge-state resolution | Merge service with risk-tier policy; branch-protection checks |
| Definition of done | ✅ Native `completion_contracts` and `work_assessments` | **Code checker library** (L1–L3, L7); **holdout-scenario runner** (L4) |
| Review and approvals | ✅ Approvals, decision queues, issue review policy | **Evidence card and inbox**; batch approval; lights-out ladder per line |
| Untrusted input | ✅ `low_trust_review` preset, low-trust runtime containment, run secret redaction | Injection red-team suite for issues, dependency diffs and docs |
| Budgets and cost | ✅ Budget policies and incidents, cost events, quota windows | **Outcome-priced usage ledger** (charge on merge; failed orders free) |
| Recovery and watchdog | ✅ Three-attempt recovery; task watchdog | Effort and model escalation on retry |
| Recurring work | ✅ Routines | Maintenance line schedules |
| Deploy targets | ◐ Vercel connect, Railway services | Preview environments, feature flags, rollback adapters |
| Evals | ✅ Runner evals and product end-to-end evals ([doc](../../evals.md)) | Per-line golden sets with holdouts; public benchmark |
| Product knowledge | ◐ Company skills, documents, memory connectors | **Product Brain** and **Repo X-ray** |

## 8. Build list (priority order)

1. Code checker library (L1–L3, L7) and the evidence card.
2. Order contract extensions on `completion_contracts`, plus "couldn't finish" outcomes.
3. Factory sandbox images (TypeScript and Python first) with an egress policy and no secrets.
4. Merge service with risk-tier policy, and the evidence inbox with batch approval.
5. Repo X-ray and the first version of the Product Brain.
6. Outcome-priced usage ledger; per-order and per-month caps.
7. Holdout-scenario runner against previews; twin services (Stripe, auth, email, storage).
8. Order sizing from measured pass rates; routing and cache telemetry; escalation on retry.
9. Lights-out ladder per line; post-merge false-green audit.
10. Per-line eval suites; public factory benchmark harness.

## Sources

- Anthropic engineering: [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) · [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- Anthropic docs: [Claude API pricing](https://platform.claude.com/docs/en/about-claude/pricing) · [Optimizing for cost and intelligence](https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence.md) · [Claude Code costs](https://code.claude.com/docs/en/costs)
- Evidence: [METR time horizons](https://metr.org/time-horizons/) · [METR on reward hacking](https://metr.org/blog/2025-06-05-recent-reward-hacking/) · [CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report) · [Veracode 2026](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/) · [DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/) · [Stack Overflow 2025](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/) · [VKTR on Claude Code Review](https://www.vktr.com/ai-news/anthropic-launches-multi-agent-code-review-for-claude-code/) · [PocketOS incident](https://www.tomshardware.com/tech-industry/artificial-intelligence/claude-powered-ai-coding-agent-deletes-entire-company-database-in-9-seconds-backups-zapped-after-cursor-tool-powered-by-anthropics-claude-goes-rogue)
- Patterns: [Simon Willison on StrongDM's factory](https://simonwillison.net/2026/Feb/7/software-factory/) · [Simon Willison: the lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/)
- Infrastructure: [Northflank sandbox pricing comparison](https://northflank.com/blog/ai-sandbox-pricing)
- This repository: `doc/execution-semantics.md`, `doc/execution-github-identity.md`, `doc/LOW-TRUST-PRESETS.md`, `doc/TASK-WATCHDOG.md`, `doc/evals.md`, `packages/adapters/`, `packages/plugins/sandbox-providers/`, `packages/db/src/schema/completion_contracts.ts`, `server/src/services/`
