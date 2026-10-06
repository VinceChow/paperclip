# [Brand] Product Requirements Document (PRD v2)

| | |
|---|---|
| **Product** | [Brand]: the AI software factory for small software companies |
| **Document** | PRD v2.0 (draft for review). Replaces [PRD v1 (OPC platform)](../2026-09-26-opc-platform/prd.md) |
| **Date** | 2026-10-04 |
| **Owner** | Founder / CPO |
| **Status** | Draft. Needs review by Engineering lead, Design lead and Security/compliance |
| **Build assumption** | **Built on a fork of Paperclip** (MIT), decision D4 in the [pivot proposal](./pivot-proposal.md#9-decisions-for-you). Paperclip supplies the control plane: issues, agents and adapters, sandboxes, workspaces, GitHub identity, approvals, budgets, contracts, routines and evals. We build the factory layer: lines, verification, the evidence inbox, the merge service, previews, the outcome-priced ledger and the factory UI |
| **Related documents** | [Market research v3](./market-research.md) · [Competitor analysis](./competitor-analysis.md) · [Factory lines](./factory-lines.md) · [Factory harness](./reliability-cost-harness.md) · [Product strategy v2](./product-feature-strategy.md) · [Marketing plan v2](./marketing-plan.md) · [X guide v2](./x-build-in-public-guide.md) |

**Placeholders:** `[Brand]` is the product name, pending naming and trademark clearance ([market research §2.2](./market-research.md#22-naming-trademarks-and-domains)).

**Requirement keywords:**
- **MUST** = required for the release it is assigned to.
- **SHOULD** = expected unless there is a documented reason not to.
- **MAY** = optional.

**Priorities:**
- **P0** = public beta (W0, week of 25 Jan 2027).
- **P1** = general availability (GA, late April 2027).
- **P2** = after GA.

---

## Table of contents

1. Summary
2. Problem and opportunity
3. Goals, non-goals and success metrics
4. Users, personas and jobs to be done
5. Product principles
6. Scope and release plan
7. Information architecture and key journeys
8. Functional requirements (16 modules)
9. AI system requirements
10. Non-functional requirements
11. System architecture (on the Paperclip fork)
12. Data model
13. Integrations and third-party dependencies
14. Plans, pricing and billing rules
15. Analytics and instrumentation
16. Security, privacy and compliance
17. Operations
18. Delivery plan
19. Risks, assumptions, dependencies and open questions
20. Appendices: line spec, schemas, acceptance scenarios, notifications, copy rules, glossary

---

## 1. Summary

[Brand] gives a small software company (a solo founder, a team of up to 20 engineers, or an agency) **a software factory**:
- issues, error events, advisories and specs go in;
- **verified, merged and released changes** come out;
- every change carries an **evidence card** proving it met its definition of done;
- agents work only in sandboxes, **can't touch production**, and escalate risky changes to a human;
- customers pay **only for changes that merge**, at a price shown before work starts. Failed work is free.

The customer doesn't configure agents or write prompts. They **decide**:
- approve a spec;
- approve a batch of Medium changes;
- approve each High change individually.

Low-risk lines earn "lights-out" operation from their measured track record. Every Friday a factory report shows what shipped, the DORA metrics, cost per change, and **what failed and why**.

**We win on five things competitors don't combine:**
1. Verified changes (tests first, holdout scenarios, scans, previews).
2. Safe by construction.
3. Decisions on evidence instead of reading diffs.
4. Predictable outcome pricing with real human support.
5. Model neutrality across every major coding agent.

---

## 2. Problem and opportunity

**The problem.** AI made writing code cheap. It did not make *shipping correct, safe software* cheap.

| Problem | Evidence | Source |
|---|---|---|
| AI changes need more fixing | About 1.7x more issues per PR; logic issues +75% | [CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report) |
| Security is not improving | A 56% security pass rate across 100+ models | [Veracode 2026](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/) |
| Speed without stability | AI raises throughput and change failures; it amplifies existing practice | [DORA 2025](https://dora.dev/insights/dora-2025-year-in-review/) |
| Review is the bottleneck | The top Hacker News theme (24%); output per Anthropic engineer up about 200% | [Market research §3.4](./market-research.md#34-what-they-struggle-with-today-two-voice-of-customer-sources) |
| Little real delegation | 0–20% of tasks fully delegated | [Anthropic](https://resources.anthropic.com/2026-agentic-coding-trends-report) |
| Unfair, unpredictable bills | 66% of negative reviews are about money; 24% say they paid for failure | [Market research §4.4](./market-research.md#44-voice-of-customer-656-negative-reviews-trustpilot) |
| Destructive accidents | Production database and backups deleted in 9 seconds | [PocketOS](https://www.tomshardware.com/tech-industry/artificial-intelligence/claude-powered-ai-coding-agent-deletes-entire-company-database-in-9-seconds-backups-zapped-after-cursor-tool-powered-by-anthropics-claude-goes-rogue) |

**The opportunity.**
- There are about **220K** core US small software companies.
- That is a US market of about **$0.5–2.6B** a year for accounts paying $200–1,000 a month, and about $2–10B globally.
- Enterprise factories (Factory, 8090) and app builders (Lovable, Replit) leave a governed, self-serve factory for 1–20-person teams open ([market research §1.6, §4](./market-research.md#16-market-sizing-order-of-magnitude-assumptions-stated)).

---

## 3. Goals, non-goals and success metrics

### 3.1 Goals

| # | Goal | Measure | Beta target | GA target |
|---|---|---|---|---|
| G1 | Value fast, without prompting | Time from repository connect to first merged, verified change (p50) | ≤ 30 min | ≤ 20 min |
| G2 | Changes are right the first time | First-pass merge rate (merged without reviewer edits) | ≥ 60% | ≥ 75% |
| G3 | No false green | Merged changes with an all-green evidence card that fail within 7 days | 0 | 0 |
| G4 | Safe by construction | Production-credential exposures to agents · High-tier changes approved by a human | 0 · 100% | 0 · 100% |
| G5 | Stability | Change-failure rate of factory changes | ≤ 15% | ≤ 10% |
| G6 | Customers keep using it | Week-4 retention of activated trials | ≥ 35% | ≥ 45% |
| G7 | Trust in billing and support | Human first response (Team and Agency, business hours) · billing tickets open > 48 h | ≤ 1 h · 0 | ≤ 1 h · 0 |
| G8 | Sustainable economics | Cost per merged Medium change (p50) · blended gross margin | ≤ $6 · ≥ 45% | ≤ $5 · ≥ 55% |

**North Star:** weekly merged, verified changes per active account.

**Customer-facing value metrics:**
- engineering hours returned (estimate; method shown);
- cost per change compared with a human.

### 3.2 Non-goals (this PRD)

- No "replace your engineers" autopilot. Level 5 is not the default; autonomy is earned per line.
- No production credentials, cloud-admin tokens or database URLs given to agents. Ever.
- No credits, compute units or opaque usage meters. No automatic overage charges.
- No new IDE or editor. No proprietary model.
- No no-code app builder for non-engineers; no hosting of customer apps.
- No general chat assistant.
- No hosted CI of our own at P0 (we use the customer's CI).
- No GitLab at P0 (P1), no Bitbucket (P2), no self-hosted or air-gapped deployment before P2.

---

## 4. Users, personas and jobs to be done

### 4.1 Primary personas

| Persona | Snapshot | Top jobs to be done | Success looks like |
|---|---|---|---|
| **Sam, solo technical founder** (P0) | 34; one B2B SaaS at $8K MRR; Next.js + Postgres | Ship the roadmap; keep dependencies and security current; fix bugs fast | A feature a week without nights; no surprise incidents; predictable cost |
| **Ines, agency owner** (P0) | 41; 6 people; 12 client repositories | More delivered per person; consistent quality; client reports and handovers | 30% more projects with the same team; fewer post-launch defects |
| **Dana, freelance developer** (P0) | 29; fixed-price projects | Finish faster at provable quality | Twice the projects; evidence to show clients |
| **Raj, startup CTO** (P1) | 38; 8 engineers | Ship faster without hiring; keep review and security under control | Throughput up; change-failure rate flat or down |

### 4.2 Secondary users

- **Reviewers:** teammates who approve Medium and High changes (P1 review routing).
- **Agency clients:** read-only evidence cards and weekly reports (P1).
- **Internal staff:** support, line authors, operations, security.

### 4.3 Context assumptions

- Customers already use GitHub with some CI. 70% or more of target repositories have a runnable test suite; the Repo X-ray checks this.
- They already use at least one coding agent. We integrate those agents; we don't replace them.
- They read evidence on desktop and approve on mobile.

---

## 5. Product principles

These are binding. Rationale: [product strategy §2](./product-feature-strategy.md#2-product-principles).

1. **Value is a verified, merged change.**
2. **Zero prompts to value.**
3. **Show evidence, not diffs.**
4. **Risk decides the interruption** (Low, Medium, High; §8.6).
5. **Safe by construction:** capabilities come from the sandbox, never from prompts.
6. **Honest by default:** show failures, never charge for them, never call something green that isn't.
7. **Autonomy is earned with evidence,** per line and per repository.
8. **Model-neutral.**
9. **Respect the owner's time.**
10. **No lock-in:** normal Git, normal CI, exportable data.

---

## 6. Scope and release plan

### 6.1 Releases

| Release | When | Audience | Scope summary |
|---|---|---|---|
| **Phase 0: concierge** | 5 Oct to mid-November 2026 | 12 design partners | Hand-operated factory on the Paperclip fork for L2 and L3; measure the go/no-go gates |
| **Internal alpha** | End of November 2026 | Team + 3 partners | L2 end-to-end on real repositories: X-ray v0, sandbox images, checker library, merge service, inbox v1 |
| **Partner alpha** | Mid-December 2026 | 12 partners (paying pilot) | L2 + L3; evidence card; usage ledger in test mode; weekly report v1 |
| **Private beta** | Mid-January 2027 | Waitlist cohorts | + L1 preview; billing live; support staffed; status page; red-team suite passes |
| **Public beta (W0)** | Week of 25 Jan 2027 | Invite waves, then open sign-up | All **P0** requirements; **L2 and L3 generally available in beta; L1 preview** |
| **GA** | Late April 2027 | Everyone | All **P1**: L1 GA, L4 Greenfield, L5 Agency; Team plan; twin services; release and rollback; Sentry intake; GitLab |
| **Later** | May 2027 onward | — | **P2:** legacy modernization, mobile, community lines, SAML, local runner GA, EU residency |

### 6.2 Scope by module

| Module | P0 (public beta) | P1 (GA) | P2 (later) |
|---|---|---|---|
| M1 Onboarding & Repo X-ray | GitHub sign-in, app install, X-ray, five suggested orders, trial | GitLab; team invites | Bitbucket |
| M2 Product Brain | Auto-built map, commands, conventions, risky paths; "What the factory knows" page | Learn from reviewer edits; versioning | Multi-repository architecture view |
| M3 Lines & orders | Line packages (L2, L3, L1 preview), order lifecycle, planner and sizing, price quotes | L1 GA, L4, L5; line settings per repository | Community lines |
| M4 Build & sandboxes | Factory images (TypeScript, Python), egress policy, routing, escalation | Twin services; more languages (Go, Ruby) | Local runner GA; GPU lines |
| M5 Verify | Checker library L1–L3 and L7; review agents; basic holdout scenarios (L1 preview) | Full holdouts; twins (L5); mutation checks | Visual regression |
| M6 Review & trust | Evidence inbox, tiers, batch approval, GitHub and Slack approvals | Lights-out ladder, sampling, review routing | Policy as code |
| M7 Merge & release | Merge service, branch-protection checks, preview environments (Vercel) | Feature flags, staged rollout, rollback; Railway and Fly | Canary analysis |
| M8 Operate | Post-merge 7-day watch, false-green audit | Sentry intake → L2 orders | Incident command |
| M9 Factory report & metrics | Weekly report, DORA metrics, line track records | Share card; client reports | Benchmarks against peers |
| M10 Channels & notifications | Web + PWA, email, GitHub, Slack | Mobile push polish | Microsoft Teams |
| M11 Plans & billing | Solo and Agency plans, outcome-priced ledger, caps, billing center, founding pricing | Team plan; bring-your-own-key mode GA; EU/UK tax | Annual enterprise contracts |
| M12 Support & status | Human support promise, help center, status page, incident notices | Onboarding calls | Community forum |
| M13 Integrations | GitHub, GitHub Issues, Linear, Vercel, Slack, Stripe (our billing) | GitLab, Jira, Sentry, Railway, Fly | Datadog, Bitbucket |
| M14 Data, privacy & IP | Export, deletion, retention, no-training, ownership terms | Privacy dashboard | EU data residency |
| M15 Safety & security controls | No secrets in sandboxes, egress allowlists, destructive-command filter, diff policy, Safety page, red team | SSO-lite; audit export | SAML SSO; customer-managed keys |
| M16 Internal tools | Line authoring, eval dashboard, cost dashboard, flags, ops console, benchmark harness (internal) | Public benchmark | — |

---

## 7. Information architecture and key journeys

### 7.1 Navigation

| Tab | Purpose | Contents |
|---|---|---|
| **Today** | What needs you now | Evidence inbox (by tier), orders in progress, morning summary |
| **Orders** | The factory floor | Board by line and state; price and cost per order; "couldn't finish" reasons |
| **Releases** | What shipped | Merged changes, previews, flags and rollouts (P1), rollbacks |
| **Quality** | Can I trust it? | Line track records, Repo X-ray, DORA trend, false-green audit |
| **Cost & Report** | Money and the weekly report | Spend against the cap, cost per change, weekly factory report |

**Settings:**
- Product Brain;
- Lines;
- Risk & trust;
- Repositories & connections;
- Plan & billing;
- Safety;
- Help (talk to a human);
- **Advanced** (hidden by default): agents, adapters, models, routines.

### 7.2 Journey A: the first 30 minutes (activation)

1. **Sign in with GitHub.**
2. **Install the [Brand] GitHub App** on 1–3 repositories. Read-only at first; write is requested only when the first order is approved.
3. **Three questions,** asked while the **Repo X-ray** runs (≤ 10 min p90):
   - deploy target;
   - risky paths;
   - who approves.
4. **X-ray results:**
   - "Tests run: ✓ (412 tests, 71% line coverage)";
   - "9 vulnerable dependencies (2 high)";
   - "3 flaky tests";
   - "No preview environment";
   - "14 open bugs, 6 likely reproducible."
5. **Five suggested orders,** each with a price and a tier. For example: "Patch 2 high advisories — Small, $3 each"; "Fix bug #231 — Medium, $12".
6. **Approve one.** A live timeline shows plan → build → verify.
7. **The evidence card arrives:** ✓ reproduction test failed before the fix, ✓ suite green, ✓ scans clean, ✓ review agents; cost $4.10; price $12.
8. **Merge.**
9. **A preview of Friday's report;** notification preferences; done.

**Activation event:** the first merged, verified change.

### 7.3 Journey B: the daily five minutes

1. A morning summary arrives by email, Slack or push: "Overnight: 4 Low changes auto-merged (dependency patches, 1 flaky test). 2 Medium ready for batch approval. 1 couldn't finish (no reproduction; details inside)."
2. Approve the batch on the phone.
3. Done.

### 7.4 Journey C: bug from an error event to a released fix (P1 with Sentry; P0 from a GitHub issue)

1. An error event or issue arrives → L2 triage.
2. A reproduction test that fails on `main`.
3. The fix.
4. Verify: suite, scans, review agents.
5. Evidence card (tier Medium).
6. Batch approval.
7. Merge through the customer's CI.
8. A 7-day watch. If the error rate on that path doesn't drop, the order is flagged for the false-green audit.

### 7.5 Journey D: feature from spec to release (L1 preview at P0, GA at P1)

1. The owner writes or dictates the need.
2. The factory drafts a spec with acceptance checks and **3 holdout scenarios**.
3. **The owner approves the spec,** and the planner quotes "4 orders: 3 Medium + 1 Small = $39."
4. Orders are built and verified.
5. The preview passes the holdouts.
6. Evidence cards are approved.
7. Behind a flag: on for the owner, then staged rollout (P1).
8. Release.

### 7.6 Journey E: maintenance going lights-out (P1)

1. After 20 consecutive Low-tier dependency patches merged without edits and zero false green, the inbox suggests: "Let L3 patch upgrades merge automatically? Evidence: 20/20, 0 reverts." The owner accepts.
2. From then on, 1 in 10 changes is sampled into the inbox.
3. Any revert drops the line back to "Ask me."

### 7.7 Journey F: Friday

1. The weekly factory report arrives by email and in the app.
2. It covers what shipped, DORA before and after, cost per change against a human estimate, and **what failed and why**.
3. The owner approves next week's maintenance plan and suggested orders.

---

## 8. Functional requirements

Each table lists ID, requirement, priority and acceptance criteria (AC). Detailed scenarios are in Appendix C.

### 8.1 M1 Onboarding and Repo X-ray (ONB)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| ONB-1 | Sign-in MUST support GitHub OAuth; email magic link SHOULD be available for agency clients (P1) | P0 | Account created ≤ 30 s |
| ONB-2 | The [Brand] GitHub App MUST be installable on selected repositories, with read-only permissions at install. Write permissions (contents, pull requests, checks) MUST be requested only when the first order is approved | P0 | Permission screen in plain language; no write permission before the first approval |
| ONB-3 | The Repo X-ray MUST: detect the stack and package managers; run the test suite in a factory sandbox; report coverage, flaky tests, vulnerable and outdated dependencies, CI and preview presence, likely-reproducible open bugs and risky paths. **It MUST NOT change anything** | P0 | p90 ≤ 10 min for repositories ≤ 200K lines; zero writes |
| ONB-4 | If the test suite can't run in standard images, the X-ray MUST say why and propose a "make tests runnable" order | P0 | Shown for 100% of failures |
| ONB-5 | The system MUST propose five suggested orders from the X-ray, each with line, size, price and tier, approvable in one tap | P0 | ≥ 1 approvable suggestion for ≥ 90% of repositories with runnable tests |
| ONB-6 | Onboarding MUST ask three questions (deploy target, risky paths, approvers) with skippable defaults | P0 | Median completion ≤ 2 min |
| ONB-7 | Trial: 14 days, no card, **10 free Medium changes** | P0 | Ledger shows trial credit; no charge at trial end without explicit plan choice |
| ONB-8 | GitLab sign-in and installation | P1 | Same as ONB-1 to ONB-5 |
| ONB-9 | Team invites with roles (owner, approver, viewer) | P1 | — |

### 8.2 M2 Product Brain (BRN)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| BRN-1 | The Brain MUST store, per repository: architecture map (modules, entry points), commands (install, build, test, run), conventions, domain glossary, risky paths and decisions | P0 | Populated from the X-ray and README for ≥ 80% of partner repositories |
| BRN-2 | Every fact MUST record provenance (repository, docs, owner, inferred) and confidence. Inferred facts are labeled until confirmed | P0 | Source shown per fact |
| BRN-3 | A "What the factory knows" page MUST allow viewing, editing and deleting facts. Changes MUST apply to the next order | P0 | Automated test: an edited command is used by the next build |
| BRN-4 | Context for an order MUST be scoped (relevant modules and conventions) within a token budget | P0 | Context-size limits per station respected |
| BRN-5 | The Brain SHOULD propose updates from repeated reviewer edits ("You changed X to Y in 4 PRs; make it a convention?") | P1 | — |
| BRN-6 | The Brain SHOULD be versioned with rollback | P1 | — |
| BRN-7 | The Brain MUST never store secrets; a detector MUST block and redact them | P0 | Secret corpus test passes |

### 8.3 M3 Lines and orders (ORD)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| ORD-1 | A **line** MUST be a versioned package (intake, stations, definition of done, risk rules, sandbox image, budgets, evals, report fields) in the teams-catalog layout ([factory lines §4](./factory-lines.md#4-anatomy-of-a-line)) | P0 | Lines load from versioned definitions; repositories pin a line version |
| ORD-2 | P0 lines: **L2 Bug, L3 Maintenance**, and **L1 Feature (preview)**. P1 adds L1 GA, **L4 Greenfield SaaS** and **L5 Agency client** | P0 / P1 | Each line passes pass^3 ≥ 85% on its golden set before release |
| ORD-3 | Intake MUST support: GitHub issues (labels), schedules (maintenance), advisories (dependency feeds), manual orders (web, Slack, CLI), and specs (L1). P1 adds Linear and Jira issues and Sentry events | P0 / P1 | — |
| ORD-4 | Orders MUST move through: queued → spec → plan → build → verify → review → merging → released → **done** / **couldn't finish** / cancelled. Each state has plain-language copy | P0 | Visible on the order card and timeline |
| ORD-5 | The **planner** MUST split work into Small or Medium orders, sized to the repository's measured first-pass merge rate ([harness §4.3](./reliability-cost-harness.md#43-order-sizing-from-metrs-horizon-data-to-each-repository)). Large orders are never built directly | P0 | No order above Medium is built; ceiling changes are logged |
| ORD-6 | Every order MUST show a **price before work starts**. Price is fixed by size (Small $3, Medium $12) and charged only on merge | P0 | Ledger tests (Appendix C) |
| ORD-7 | Each trigger event MUST create at most one order per line (idempotency key) | P0 | Duplicate webhook test passes |
| ORD-8 | Orders MUST respect per-repository concurrency and per-day limits | P0 | Configurable per plan |
| ORD-9 | **Couldn't finish** MUST end with a reason, what was tried, partial work (branch link) and a suggested next step. It MUST NOT be charged | P0 | Ledger shows no charge |
| ORD-10 | For L1, the spec station MUST draft acceptance checks and 3 holdout scenarios, and the owner MUST approve the spec before planning | P0 (preview) | Holdouts stored outside the repository |
| ORD-11 | Line settings per repository (enable or disable, schedules, path rules) | P1 | — |

### 8.4 M4 Build and sandboxes (BLD)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| BLD-1 | Every build MUST run in an isolated factory sandbox (via Paperclip sandbox providers) with the repository at the order's base commit | P0 | No build runs on the controller host |
| BLD-2 | Factory images MUST cover TypeScript/Node (npm, pnpm, yarn) and Python (pip, uv, poetry) at P0, and Go and Ruby at P1 | P0 / P1 | ≥ 70% of partner repositories run tests without custom setup |
| BLD-3 | Sandboxes MUST have **no production secrets** mounted, and MUST enforce an egress allowlist (package registries, the git host, documentation domains) | P0 | Red-team tests (SEC-3) pass |
| BLD-4 | The build MUST write the order's tests first and prove they fail on the base commit before writing the implementation (L1, L2) | P0 | Evidence card shows "failed before" |
| BLD-5 | Station-to-model routing MUST be configurable per line (default: small model for triage, mid for build and review, frontier for plan and escalation), changeable without redeploying | P0 | Registry change takes effect on the next order |
| BLD-6 | On a failed verification, the build MUST revise with the failed criteria (≤ 2 revisions) and escalate model or effort once. It stops at 3 attempts | P0 | Trace shows attempts |
| BLD-7 | The per-order dollar cap and wall-clock limit MUST be enforced; when hit, the order ends as couldn't finish (free) | P0 | Test with a low cap |
| BLD-8 | Any supported Paperclip adapter (Claude Code, Codex, Cursor, Gemini, OpenCode and others) MAY be selected per station | P0 | Adapter shown in the evidence card |
| BLD-9 | **Twin services** (Stripe, auth providers, email, object storage) MUST be available inside sandboxes for integration paths | P1 | Twins pass compatibility tests against official client libraries |
| BLD-10 | Local-runner mode (agents on the customer's machine; control plane in the cloud) | P2 | Provider terms reviewed per adapter |

### 8.5 M5 Verify (VER)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| VER-1 | **L1:** build, typecheck, lint and format MUST pass | P0 | — |
| VER-2 | **L2:** new tests MUST fail on the base commit and pass after the change; the full suite MUST pass | P0 | — |
| VER-3 | **L3:** SAST, dependency audit, secret scan and license scan MUST show no new high or critical findings | P0 | Scanner versions pinned per image |
| VER-4 | **L4 holdout scenarios** MUST run against the preview environment, hidden from the builder (basic runner at P0 for the L1 preview; full at P1) | P0 / P1 | Holdouts not readable from the sandbox |
| VER-5 | **L6 review agents** (correctness, security) MUST run in a fresh context and post findings as a GitHub review | P0 | Blocking findings fail the order |
| VER-6 | **L7 diff policy** MUST enforce size limits (default ≤ 400 changed lines) and raise the tier when CI configuration, test configuration, lockfiles (outside L3) or migrations change | P0 | — |
| VER-7 | **No false green:** an order may be marked verified only when every required criterion passes | P0 | Invariant test; audit query returns 0 violations |
| VER-8 | Reward-hacking guards: test files written in the tests-first step are locked during implementation; deleting or skipping tests fails the order | P0 | Red-team test passes |
| VER-9 | Mutation check on changed lines for coverage jobs (L3) | P1 | — |
| VER-10 | A **false-green audit** MUST run for 7 days after merge (CI on `main`, reverts, linked incidents, holdout re-run) | P0 | Weekly report shows the audit |

### 8.6 M6 Review and trust (REV)

**Risk tiers (REV-1):**

| Tier | Definition | Default handling |
|---|---|---|
| **Low** | Docs, tests, refactors fully covered by tests, dependency patch versions, lint fixes | Auto-merge once the line is trusted (P1); batch approval until then |
| **Medium** | Features behind flags, minor upgrades, UI changes, bug fixes outside high-risk paths | Batch approval |
| **High** | Schema migrations, authentication, payments, permissions, infrastructure, CI configuration, deleting data, secrets | Individual approval, every time; **never automatic in P0 or P1** |

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| REV-1 | Every order MUST receive a tier from line rules plus path rules; customers can raise a tier, never lower a High path below High | P0 | Tier stored on the order |
| REV-2 | The **evidence inbox** MUST group by tier. Medium supports batch approval; High requires individual approval. Each card shows: order, checks ✓/✗, holdout results, scans, preview link, cost, price, attempts, model route; the diff is one click away | P0 | Median decision ≤ 60 s for Medium in usability tests |
| REV-3 | Actions MUST include approve, request change (text or voice), and reject with a reason. Rejections and edits become eval candidates | P0 | — |
| REV-4 | Approval MUST be possible from the inbox, the GitHub PR (approving review), or Slack (signed, single-use links that expire in 72 h). High tier MUST open a confirmation page | P0 | Security review passed |
| REV-5 | The **lights-out ladder** per line and repository: Draft only → Ask me → Auto with daily digest. Promotion is suggested after ≥ 20 consecutive merges without edits, zero false green and revert rate ≤ 2%. It never applies to High | P1 | The suggestion shows the evidence |
| REV-6 | Auto-merged changes MUST be sampled (1 in 10) into the inbox for spot checks | P1 | — |
| REV-7 | Any revert or false green MUST demote the line one step automatically and notify the owner | P1 | — |
| REV-8 | Review routing to named approvers by path (CODEOWNERS-aware) | P1 | — |
| REV-9 | An append-only **activity log** MUST record every action in plain language (who, what, why, evidence, tier, decision), filterable and exportable | P0 | — |

### 8.7 M7 Merge and release (REL)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| REL-1 | Merges MUST be performed only by the **merge service** (a separate identity) after the tier decision, never by build agents | P0 | Build identity lacks merge permission (test) |
| REL-2 | The merge service MUST respect branch protection and required CI checks; it MUST NOT bypass them | P0 | Test with protected branches |
| REL-3 | Preview environments MUST be created per order where the repository deploys to Vercel (P0); Railway and Fly at P1 | P0 / P1 | Preview URL on the evidence card |
| REL-4 | Feature-flag integration and staged rollout (owner first, then a percentage) | P1 | — |
| REL-5 | Automatic rollback on failed post-release health checks, with notification | P1 | Rollback test |
| REL-6 | **Destructive migrations** (dropping tables or columns, deleting data) MUST be High tier, MUST include a backup and restore plan in the evidence card, and MUST never auto-run | P0 | Diff policy plus a migration parser |

### 8.8 M8 Operate (OPS)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| OPS-1 | Every merged change MUST be watched for 7 days: CI on `main`, reverts, linked errors | P0 | Feeds VER-10 |
| OPS-2 | Sentry intake: new issues above a threshold become L2 orders; regressions link back to the change that caused them | P1 | — |
| OPS-3 | Incident notices: when a factory change is implicated in an incident, the owner is notified within 15 minutes and a rollback is offered | P1 | — |

### 8.9 M9 Factory report and metrics (RPT)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| RPT-1 | A **weekly factory report** MUST be generated on Fridays (configurable) in the app and by email. It covers: what shipped; the four DORA metrics before and after; first-pass merge rate; cost per change; lights-out share; **what failed and why**; next week's suggestions | P0 | Delivered to ≥ 99% of active accounts |
| RPT-2 | **Engineering hours returned** MUST be computed as standard minutes per line and size (from Phase 0 time studies) × merged changes, adjustable by the owner, and always labeled an estimate with the method shown | P0 | — |
| RPT-3 | **Line track records** (first-pass merge, false green, change-failure, revert rate, lights-out status) MUST be visible per repository | P0 | — |
| RPT-4 | A morning summary at a configurable time | P0 | — |
| RPT-5 | A share card for the weekly report with owner-controlled redaction (used for build-in-public) | P1 | — |
| RPT-6 | Read-only client reports for agencies | P1 | — |
| RPT-7 | The weekly report SHOULD show **autonomy** (the share of merged changes with no human code push) and **cost per merged change by size and by component** (inference, compute) ([competitor analysis C12](./competitor-analysis.md#8-what-this-changes-in-our-plan-recommendations)) | P1 | — |

### 8.10 M10 Channels and notifications (CHN)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| CHN-1 | A responsive web app and installable PWA | P0 | Lighthouse PWA checks pass |
| CHN-2 | Email notifications and approval links | P0 | — |
| CHN-3 | GitHub: PR descriptions carry the evidence-card summary and a "Generated by [Brand]" label; reviews and check runs are posted | P0 | — |
| CHN-4 | Slack: summaries, evidence cards and approvals | P0 | — |
| CHN-5 | A CLI to create orders and see status | P0 | `[brand] order "…"` works on macOS and Linux |
| CHN-6 | Notification preferences per type and quiet hours | P0 | — |
| CHN-7 | Microsoft Teams | P2 | — |

### 8.11 M11 Plans and billing (BIL)

See §14 for plan details.

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| BIL-1 | Plans Solo and Agency (P0) and Team (P1), monthly and annual, plus founding-member pricing | P0 / P1 | — |
| BIL-2 | **Outcome-priced ledger:** per-order price quote; charge only on merge; couldn't-finish and cancelled orders free | P0 | Ledger reconciles with order outcomes (daily job) |
| BIL-3 | A **hard monthly cap** set by the customer. At 80% and 100% the owner is notified. At 100%, new orders wait for approval and **nothing is charged beyond the cap** | P0 | Cap test |
| BIL-4 | A **billing center:** plan, next charge, invoices, per-change charges, cap, payment method; plan changes with proration; **pause** (up to 3 months); **cancel in ≤ 2 clicks** | P0 | Usability test: cancel ≤ 30 s |
| BIL-5 | An email 3 days before every renewal or trial-to-paid charge | P0 | — |
| BIL-6 | Refunds: monthly plans cancel anytime with no further charges; annual plans get a prorated refund of unused months on request | P0 | Policy published |
| BIL-7 | Grandfathering: existing customers keep their prices for ≥ 12 months after any change | P0 | Plan versions supported |
| BIL-8 | **Bring-your-own-key mode:** customer-supplied model API keys, stored encrypted; no per-change fee; platform fee per plan; per-order caps still enforced | P0 (Solo, Agency) / P1 (Team) | Keys never logged; usage visible |
| BIL-9 | Sales tax and VAT via the payment platform's tax service (US at P0; UK and EU at P1) | P0 / P1 | — |
| BIL-10 | Automatic account credits when we breach our promises (support, incident notices) | P1 | — |

### 8.12 M12 Support and status (SUP)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| SUP-1 | **"Talk to a human"** on every screen. Human first response ≤ **1 business hour** (Team, Agency) and ≤ 4 business hours (Solo, trial). Business hours: Mon–Fri, 8 a.m.–8 p.m. US Eastern at launch | P0 | Measured weekly |
| SUP-2 | An AI help assistant answers from the docs and hands over to a human after 2 unhelpful turns or on request | P0 | — |
| SUP-3 | A support console with read-only views of orders, evidence, ledger and errors. Viewing repository content requires the customer's in-app consent and is audited | P0 | — |
| SUP-4 | A public status page per subsystem (app, orders, sandboxes, GitHub integration, billing) with in-app incident banners | P0 | — |
| SUP-5 | Affected customers notified within 30 minutes of a confirmed incident; a postmortem for Sev-1 within 5 business days | P0 | — |
| SUP-6 | Docs: line guides, the Safety page, the pricing explainer, and 60-second videos per line | P0 | — |

### 8.13 M13 Integrations (INT)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| INT-1 | A Connections page MUST show status, the permissions we use (in plain language), reconnect and disconnect. Disconnecting revokes tokens and pauses dependent orders | P0 | — |
| INT-2 | Health monitoring MUST detect broken connections within 15 minutes, pause affected orders and show a one-tap fix | P0 | — |
| INT-3 | The provider list per release is in §13 | — | — |

### 8.14 M14 Data, privacy and IP (DATA)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| DATA-1 | **Export everything:** orders, evidence, Brain, reports, ledger (JSON + CSV), self-serve, delivered within 24 h | P0 | — |
| DATA-2 | **Account deletion** MUST revoke tokens immediately and purge data within 30 days (backups within 90) | P0 | — |
| DATA-3 | Repository content in sandboxes MUST be deleted when the order ends. Logs and traces are redacted and kept 30 days by default | P0 | Sandbox teardown verified |
| DATA-4 | Customer code and data MUST NOT be used to train models. Model providers MUST be under no-training terms, with zero data retention where available | P0 | Contracts on file |
| DATA-5 | Terms MUST state that the customer owns all output. The activity log records human-approved specs and edits; this supports customers' copyright position on AI-assisted work | P0 | Legal review |
| DATA-6 | A privacy dashboard ("what we store, per repository") | P1 | — |
| DATA-7 | EU data residency | P2 | — |

### 8.15 M15 Safety and security controls (SEC)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| SEC-1 | Build and verify agents MUST NOT receive production credentials, cloud-admin tokens or database URLs | P0 | Secret scan of sandbox environments in CI; red-team test |
| SEC-2 | GitHub access MUST use Paperclip's managed, token-free launchers bound to the run's identity. Credentials are never persisted in the sandbox | P0 | — |
| SEC-3 | Egress allowlists per image. Untrusted input (issue text, dependency diffs, web content) MUST be handled under the low-trust preset. No single step may combine private data, untrusted content and open egress | P0 | Injection red-team suite passes |
| SEC-4 | A destructive-command filter (deleting outside the workspace, `DROP`/`TRUNCATE` against non-test databases, force-push, branch or volume deletion) | P0 | — |
| SEC-5 | A Safety page MUST list what agents can and cannot do, for customers' security reviews | P0 | — |
| SEC-6 | SSO-lite (Google Workspace and GitHub organization enforcement) and audit-log export | P1 | — |
| SEC-7 | SAML SSO; customer-managed keys | P2 | — |

### 8.16 M16 Internal tools (ADM)

| ID | Requirement | Pri | Acceptance criteria |
|---|---|---|---|
| ADM-1 | Line authoring with versioning, eval runs and staged rollout by account cohort | P0 | — |
| ADM-2 | An eval dashboard per line: golden set, pass@1, pass^3, false-green audits, reviewer-agent agreement with humans. **Deploys that change prompts, models or lines MUST be blocked on regression** | P0 | CI gate |
| ADM-3 | A cost dashboard: cost per order, line, account; cache hit rate; anomalies (an account above 2x the line's p90) | P0 | Alerting |
| ADM-4 | Feature flags and per-account staged rollouts | P0 | — |
| ADM-5 | An ops console to inspect, retry and cancel orders, with redacted traces | P0 | — |
| ADM-6 | An internal benchmark harness (public at P1) | P0 / P1 | — |
| ADM-7 | **Replay and self-improvement:** before a model or line version rolls out to an account, replay a sample of that account's past orders on the candidate and compare cost, first-pass merge and holdout pass rates. Group repeated holdout failures, false greens and reverts into proposed line changes, with evidence, for line owners to review ([competitor analysis C11](./competitor-analysis.md#8-what-this-changes-in-our-plan-recommendations)) | P1 | No line version reaches an account cohort without a replay result |

---

## 9. AI system requirements

### 9.1 Approach

- **Stations are deterministic pipelines with agent steps.** Spec, plan, build and review use agents. Checks are code.
- **Order-sized work.** No long-running "do everything" sessions.
- **No always-on agents or tight heartbeats.** Work is triggered by events, schedules or approvals ([harness §6.3](./reliability-cost-harness.md#63-cost-per-change-assumptions-stated)).

### 9.2 Model routing (initial; revised per line using the eval dashboard)

| Station | Default | Notes |
|---|---|---|
| Triage, classification, log summary | Small (Claude Haiku 4.5) | Structured outputs |
| Build, fix, review agents | Mid (Claude Sonnet 5.5) or an equivalent adapter | Measured by cost per merged change |
| Spec, plan, escalation | Frontier (Claude Opus 5.5) | Fable 5.1 only for the hardest escalations |
| Other adapters (Codex, Gemini, Cursor, OpenCode) | Per-line A/B | Chosen on measured first-pass merge rate and cost |

| ID | Requirement |
|---|---|
| AI-1 | A model and adapter registry MUST allow per-station changes without redeploying |
| AI-2 | Model, prompt or adapter changes MUST pass line regression evals (ADM-2) |
| AI-3 | Prompt assembly MUST be cache-stable (system → tools → Product Brain → line instructions; volatile content after the breakpoint). Target ≥ 70% of input tokens read from cache on build stations |
| AI-4 | Batch processing MUST be used for X-ray refreshes, reports and eval runs |
| AI-5 | Every order MUST carry a dollar cap; every account a monthly guard at 2x expected cost that triggers review (not a customer charge) |
| AI-6 | Output-token limits MUST NOT truncate agentic runs (≥ 64K with streaming) |
| AI-7 | Cost targets: Medium change ≤ $6 at p50 (beta) and ≤ $5 (GA); p90 ≤ $12 |
| AI-8 | Each line MUST have a golden set of 20–50 real (consented) tasks with holdout scenarios before release |
| AI-9 | Lines MUST reach pass^3 ≥ 85% before release, and meet G2 on live traffic |
| AI-10 | Reviewer agents MUST be calibrated to ≥ 85% agreement with human labels on blocking findings |
| AI-11 | A weekly transcript review (25 orders per line) MUST be part of operations |
| AI-12 | **Untrusted input:** issue text, comments, dependency diffs and fetched docs are data, never instructions. Steps that read untrusted content MUST NOT have open egress or secrets |
| AI-13 | Tool allowlists per station; no general network access beyond the image's allowlist |
| AI-14 | A red-team suite (injection in issues and READMEs, malicious dependency diffs, test-tampering prompts, secret-exfiltration attempts) MUST pass before each release |
| AI-15 | Logs and traces MUST redact secrets and personal data by default; access is role-based and audited |

---

## 10. Non-functional requirements

| Category | ID | Requirement |
|---|---|---|
| **Performance** | NFR-1 | Web app p75 Largest Contentful Paint ≤ 2.0 s; interaction p75 ≤ 200 ms |
| | NFR-2 | Inbox approvals acknowledged ≤ 300 ms; batch of 20 ≤ 1 s |
| | NFR-3 | Webhook ingestion to order start: p90 ≤ 30 s |
| | NFR-4 | Sandbox ready (image cached): p90 ≤ 60 s |
| | NFR-5 | Repo X-ray p90 ≤ 10 min (≤ 200K lines) |
| **Availability** | NFR-6 | App and API 99.9% monthly; webhook endpoints 99.95% with provider redelivery |
| | NFR-7 | **No lost events:** at-least-once ingestion, idempotent processing, outbox for side effects (merges, charges) |
| | NFR-8 | Recovery point ≤ 15 min; recovery time ≤ 4 h; quarterly restore drills |
| **Scalability** | NFR-9 | GA design point: 5,000 accounts, 300K orders a month, 500 concurrent sandboxes; horizontally scalable workers |
| **Security** | NFR-10 | OWASP ASVS Level 2; third-party penetration test before GA; bug bounty after GA |
| | NFR-11 | Tokens and model keys encrypted with envelope encryption; never logged |
| | NFR-12 | Tenant isolation enforced at the database (company scoping, per Paperclip invariants) with automated cross-tenant tests |
| | NFR-13 | Staff access via SSO with MFA, least privilege, just-in-time elevation, audited |
| **Compliance** | NFR-14 | SOC 2 Type I by GA; Type II within 12 months of GA |
| **Accessibility** | NFR-15 | WCAG 2.2 AA; keyboard navigation for the inbox |
| **Compatibility** | NFR-16 | Last 2 versions of Chrome, Edge, Firefox and Safari; iOS 17+ and Android 12+ |
| **Observability** | NFR-17 | Tracing across ingestion → order → sandbox → provider calls; per-order cost and latency; SLO alerting (Paperclip's OpenTelemetry path, operator-gated) |

---

## 11. System architecture (on the Paperclip fork)

### 11.1 Overview

```
        ┌──────────────── Clients ────────────────┐
        │ Factory web app / PWA · Slack · GitHub  │
        │ (PRs, checks, reviews) · Email · CLI    │
        └───────────────┬─────────────────────────┘
                        │
            ┌───────────▼────────────┐        ┌─────────────────────────┐
            │ Factory API (new)      │◄──────►│ Paperclip server (fork) │
            │ orders, inbox, ledger, │        │ issues, agents/adapters,│
            │ X-ray, Brain, reports  │        │ approvals, budgets,     │
            └───┬───────────┬────────┘        │ contracts, routines,    │
                │           │                 │ activity log, evals     │
   webhooks ────┘           │                 └───────────┬─────────────┘
   (GitHub, Linear,         │                             │ runs
    Sentry, Vercel)         ▼                             ▼
            ┌───────────────────────┐        ┌─────────────────────────────┐
            │ Merge service (new)   │        │ Runner + sandbox providers  │
            │ separate identity;    │        │ (E2B / Daytona / Modal …)   │
            │ tier policy; branch   │        │ factory images · egress     │
            │ protection; outbox    │        │ allowlist · twin services   │
            └──────────┬────────────┘        │ · checker library · holdout │
                       │                     │ runner (scenarios hidden)   │
                       ▼                     └──────────────┬──────────────┘
            GitHub / GitLab (customer repos, CI)            │ model calls
            Vercel / Railway / Fly (previews, releases)     ▼
                                              Claude API · other agent providers
 Data: Postgres (Paperclip schema + factory tables) · object storage (evidence artifacts, logs)
       · analytics · traces · eval store · Stripe (billing)
```

### 11.2 Components

| Component | Reused from Paperclip | New for the factory |
|---|---|---|
| Orders | Issues, sub-issues, blockers, plan decompositions, execution policy | Order model (size, price, line, tier), planner and sizing |
| Agents | Adapter registry (12 adapters), AI connection defaults, quota windows | Per-station routing; cost per merged change |
| Execution | Execution workspaces, runtime leases, sandbox providers, execution allowlist, runner | Factory images, egress presets, twin services |
| GitHub | Managed launchers, run identity, review checks, PR reviews, merge-state resolver | Merge service; branch-protection checks; PR evidence summary |
| Verification | Completion contracts, work assessments, native completion reviews | Checker library, holdout runner, false-green audit |
| Decisions | Approvals, decision queues, issue review policy, training examples | Evidence inbox, batch approval, lights-out ladder |
| Budgets and cost | Budget policies and incidents, cost events | Outcome-priced ledger, Stripe billing, caps |
| Recurring work | Routines, task watchdog | Maintenance schedules |
| Chat | Slack and GitHub chat surfaces | Evidence cards in Slack |
| UI | React + Vite board UI, design system ([`DESIGN.md`](../../../DESIGN.md)) | Factory shell (Today, Orders, Releases, Quality, Cost & Report); Advanced keeps Paperclip views |

### 11.3 Stack decisions

| Area | Decision | Why |
|---|---|---|
| Base | Paperclip fork (TypeScript, Express API, React + Vite UI, Drizzle + Postgres) | D4; most of the control plane exists |
| Fork strategy | Thin fork: factory code in new packages (`packages/factory-*`, `server/src/factory/*`); weekly upstream merge; contribute general fixes upstream | Limits merge cost |
| Sandboxes | E2B or Daytona primary (about $0.17 an hour for 2 vCPU / 4 GiB), Modal as a secondary; via Paperclip providers | Price parity; already integrated |
| Models | Claude API (Haiku 4.5, Sonnet 5.5, Opus 5.5) plus other adapters | Routing by measured cost per merged change |
| Scanners | Open-source scanners in images (SAST, dependency audit, secrets, licenses); pinned versions | Cost and portability |
| Billing | Stripe Billing + Stripe Tax; our ledger computes per-change charges as metered usage | Proven; supports caps and proration |
| Support and status | Plain or Intercom; Instatus | Buy |
| Analytics | PostHog | One tool for events and flags |
| Hosting | Managed Postgres, containers on AWS (or GCP), infrastructure as code | SOC 2-friendly |

### 11.4 Key sequence: L2 bug order

1. GitHub `issues.labeled(bug)` webhook → order created (idempotency key = issue ID + line).
2. Triage (small model) → reproducible? Yes → size Medium → price $12 shown. The auto-run policy applies to bugs, or the order waits for approval.
3. A sandbox starts from the image with the repository at `main` and no secrets.
4. The reproduction test is written → it fails on `main` (asserted) → the test file is locked.
5. The fix is written → verify L1–L3 and L7 → review agents (L6).
6. All green → evidence card → inbox (Medium, batch). The owner approves.
7. The merge service merges after required CI passes → ledger charges $12 → the 7-day watch starts.
8. If CI on `main` fails, or a revert happens within 7 days → the false-green flag, a new L2 order, the line track record is updated, and **the charge is refunded**.

### 11.5 Key sequence: maintenance lights-out (P1)

1. The weekly L3 routine checks advisories and outdated dependencies → creates Small orders.
2. Each order builds and verifies.
3. The line is in "Auto with digest" for patch upgrades → the merge service merges.
4. 1 in 10 changes is sampled into the inbox.
5. The daily digest lists the merges with their evidence.

---

## 12. Data model

**New factory tables.** Every row carries `company_id`, enforced by Paperclip's company-scoping invariants.

| Entity | Key fields | Notes |
|---|---|---|
| **Repository** | id, provider, external_id, default_branch, install_id, xray_status | Links to Paperclip `projects` and `project_workspaces` |
| **XrayReport** | repository_id, findings (JSON), test_runnable, coverage, created_at | ONB-3 |
| **BrainFact** | repository_id, section, key, value (JSON), provenance, confidence, confirmed_at, version | BRN-* |
| **Line / LineVersion** | key, version, definition (YAML/JSON), status | ORD-1 |
| **RepositoryLineSetting** | repository_id, line_key, enabled, schedule, trust_level | REV-5 |
| **Order** | id, issue_id (Paperclip), line, size, price_usd, tier, state, attempts, cost_usd, outcome, reason | Maps to a Paperclip issue |
| **OrderContract** | order_id, completion_contract_id (Paperclip), criteria (JSON), holdout_ref | Extends `completion_contracts` |
| **CheckResult** | order_id, criterion_id, tier (L1–L7), pass, details_ref, attempt | VER-* |
| **HoldoutScenario** | spec_id, scenario (Given/When/Then plus script), visibility = hidden | VER-4 |
| **EvidenceCard** | order_id, summary (JSON), preview_url, pr_url, cost_usd, model_route | REV-2 |
| **MergeEvent** | order_id, merged_by (service identity), commit_sha, ci_status | REL-1 |
| **WatchResult** | order_id, ci_on_main, reverted, linked_incidents, false_green | VER-10 |
| **LedgerEntry** | company_id, order_id, kind (quote / charge / refund / trial_credit), amount_usd, period | BIL-2 |
| **Plan / Subscription** | plan, plan_version, mode (managed / bring-your-own-key), cap_usd, status, trial_ends_at | BIL-* |
| **ModelKey** | company_id, provider, encrypted_key_ref, last_used_at | BIL-8 |
| **WeeklyReport** | company_id, week_start, metrics (JSON), content_ref | RPT-1 |
| **LineTrackRecord** | repository_id, line_key, window, first_pass_rate, false_green, revert_rate, cfr | RPT-3 |
| **EvalCase** | line_key, source (golden / edit / reject / revert), repo_ref, expected, labels, consent | AI-8 |
| **SupportTicket** | id, priority, first_response_at, resolved_at | SUP-1 |

**Reused Paperclip tables:**
- issues, issue relations, plan decompositions;
- agents, adapters, runs, run events;
- approvals, decisions, decision queues, training examples;
- budget policies and incidents, cost events;
- completion contracts, work assessments;
- execution workspaces;
- routines, activity log.

The schema workflow follows [`AGENTS.md` §6](../../../AGENTS.md).

---

## 13. Integrations and third-party dependencies

| Provider | Use | Release | Lead-time and approval risks |
|---|---|---|---|
| **GitHub App** | Repositories, issues, PRs, checks, reviews | P0 | Fine-grained permissions review; rate limits (installation tokens, conditional requests). GitHub Marketplace listing is optional, and its review takes weeks, so submit by December 2026 |
| GitHub Issues · Linear | Intake | P0 | Linear OAuth app review |
| **Vercel** | Preview environments | P0 | Vercel integration review: **submit in November 2026**; fallback is customer-provided preview URLs |
| Slack | Notifications, approvals | P0 | Slack app review for public distribution: submit in December 2026 |
| **Stripe Billing + Tax** | Our billing | P0 | — |
| **Sandbox providers** (E2B, Daytona, Modal) | Execution | P0 | Data processing agreements; region choice; capacity reservations before launch |
| **Model providers** (Anthropic and others) | Agent stations | P0 | No-training and zero-data-retention terms; rate-limit tier increases before W0 |
| GitLab | Code host | P1 | — |
| Jira | Intake | P1 | Atlassian app review |
| **Sentry** | Error intake | P1 | Sentry integration platform review |
| Railway · Fly | Previews and releases | P1 | — |
| Feature flags (built-in plus LaunchDarkly or Unleash adapters) | Staged rollout | P1 | — |
| Datadog · Bitbucket · Microsoft Teams | — | P2 | — |
| **SOC 2 auditor plus compliance automation** | Type I by GA | Start October 2026 | Controls must run for the Type I point in time; pick a vendor in October |

---

## 14. Plans, pricing and billing rules

Consistent with [market research §6.3](./market-research.md#63-pricing-recommendation-decision-d5-to-validate-in-phase-0). Prices are hypotheses until the Phase 0 pricing test.

| | **Solo** | **Team** (P1) | **Agency** |
|---|---|---|---|
| Platform fee, Managed mode | $29 / month | $199 / month (5 seats; +$29 per extra seat) | $399 / month (10 seats) |
| Platform fee, bring-your-own-key mode | $79 / month | $399 / month | $799 / month |
| Per merged change (Managed) | Small $3 · Medium $12 | Same | Same |
| Repositories | 3 | 20 | Unlimited client workspaces |
| Lines | L1–L4 as released | L1–L4 | L1–L5 |
| Support | Human reply ≤ 4 business hours | ≤ 1 business hour | ≤ 1 business hour + onboarding call |
| Annual billing | 20% off platform fee | Same | Same |

**Always included:**
- failed or cancelled orders are free;
- the price is shown before work starts;
- a hard monthly cap set by you;
- cost per change on every card;
- one-click cancel and pause;
- no overage charges ever.

**Rules:**
1. **Size is set by the planner,** not the customer. Large work is split into Medium orders, each priced before approval.
2. **Charge on merge.** If a false green is found within 7 days, the charge is **refunded automatically** and a fix order is created free.
3. **Trial:** 14 days, no card, 10 free Medium changes.
4. **Founding members (first 500 accounts):** 40% off the platform fee for year one.

**Unit economics:** see [harness §6.3](./reliability-cost-harness.md#63-cost-per-change-assumptions-stated). Gross margin is about 52% (Solo), 58% (Team) and 59% (Agency).

---

## 15. Analytics and instrumentation

### 15.1 Event taxonomy

All events carry `company_id`, `user_id`, `plan`, `mode` and `platform`. Order events also carry `line`, `size` and `tier`.

| Area | Events |
|---|---|
| Onboarding | `signup_completed`, `app_installed{repos}`, `xray_completed{test_runnable, findings}`, `suggested_order_approved`, `first_merge` |
| Orders | `order_created{trigger}`, `order_state_changed`, `order_merged{attempts, cost, duration}`, `order_couldnt_finish{reason}`, `check_result{tier, pass}` |
| Review | `card_viewed`, `decision_made{action, latency_ms, batch_size, diff_opened}`, `change_requested`, `trust_promotion_suggested/accepted`, `line_demoted{reason}` |
| Release and operate | `preview_ready`, `merged`, `rollback`, `false_green_detected`, `incident_linked` |
| Report | `weekly_report_sent`, `weekly_report_opened`, `share_card_created` |
| Billing | `trial_started`, `plan_selected{mode}`, `cap_set`, `cap_80`, `cap_100`, `charge`, `refund{reason}`, `pause`, `cancel_completed{reason}` |
| Support | `help_opened`, `ai_help_escalated`, `ticket_first_response{minutes}` |

### 15.2 Dashboards

- **North Star:** weekly merged, verified changes per active account.
- **Activation:** app install → X-ray → first approved order → first merge → 3 merges in week 1.
- **Reliability:** first-pass merge rate, false green, couldn't-finish rate, pass^3 per line, change-failure rate.
- **Review:** decision latency; share of decisions with the diff opened.
- **Economics:** cost per merged change (p50 and p90), cache hit rate, gross margin by plan and mode.
- **Trust:** support first response, billing tickets, refunds, cancellations with reasons.

---

## 16. Security, privacy and compliance

| Area | Requirement | Owner and timing |
|---|---|---|
| **SOC 2** | Type I by GA; Type II within 12 months of GA | Start controls October 2026 |
| **Penetration test** | Third party before GA; yearly retest; scope includes sandbox escape and injection | P1 gate |
| **Secure development** | Threat model for sandboxes, merge service and ledger; dependency pinning; signed builds | P0 |
| **GDPR / UK GDPR / CCPA** | Data processing agreement, subprocessor list (sandbox and model providers), data-subject requests | P0 |
| **No training; retention** | DATA-3, DATA-4 | P0 |
| **Open-source license compliance** | License scan on new dependencies; customer policy (deny GPL in proprietary repositories, for example) | P0 |
| **IP and copyright** | Customer owns output; human approvals recorded; terms reviewed by counsel ([Copyright Office](https://newsroom.loc.gov/news/copyright-office-releases-part-2-of-artificial-intelligence-report/s/f3959c36-d616-498d-b8f9-67641fd18bab)) | P0 |
| **EU Cyber Resilience Act** | We aren't the manufacturer of customers' products. We support customers' duties with SBOM export and vulnerability-handling evidence (reporting from 11 Sep 2026; full application 11 Dec 2027) ([EC](https://digital-strategy.ec.europa.eu/en/policies/cra-reporting)) | P1 SBOM export; P2 vulnerability workflow |
| **AI transparency** | PRs and commits created by the factory are labeled "Generated by [Brand]" | P0 |
| **FTC (advertising)** | No unproven productivity or "replace engineers" claims; testimonials rules | P0 (marketing review) |
| **Payments (PCI)** | Stripe-hosted only | P0 |
| **Incident response** | Runbook, on-call, customer notice ≤ 30 min, breach notification per law | P0 |

---

## 17. Operations

| Area | Plan |
|---|---|
| **Support staffing** | Beta: founder plus 1 support/DevRel lead. GA: 1 support engineer per about 500 paying accounts (assumption). Humans handle billing, trust and failed orders; the AI assistant handles how-to questions |
| **On-call** | Weekly engineering rotation. Sev-1 response ≤ 15 min, 24/7 for the merge service, ledger and webhooks |
| **Line operations** | Each line has an owner who reviews 25 orders a week, grows the golden set from edits, rejections and reverts, and ships line versions through staged rollout |
| **Model operations** | Monthly routing and caching review per line. Re-audit prompts on model migrations. Evals gate every change |
| **Sandbox operations** | Image rebuilds weekly with pinned scanners; capacity planning; orphan cleanup (Paperclip's sandbox orphan cleanup) |
| **Abuse** | Terms prohibit malware and credential stuffing tools. Automated detection of abusive orders, with a manual review queue |
| **Upstream** | Weekly upstream Paperclip merge; a fork-health dashboard (conflicts, drift) |

---

## 18. Delivery plan

### 18.1 Team

| Role | Count | Starts |
|---|---|---|
| Founder / CPO (product, lines, go-to-market, build in public) | 1 | Now |
| Engineering lead (Paperclip fork, platform, merge service) | 1 | October 2026 |
| Product engineers (factory API and UI, inbox, ledger, reports) | 2 | October 2026 |
| AI / agents engineer (lines, routing, evals, review agents) | 1 | October 2026 |
| Infrastructure and security engineer (sandbox images, egress, twins, SOC 2 controls) | 1 | October 2026 |
| Integrations engineer (GitHub App, Vercel, Slack, Linear, Stripe) | 1 | October 2026 |
| Product designer | 1 | October 2026 |
| Support / DevRel lead | 1 | December 2026 |
| Fractional: security (penetration test), legal, QA | — | As needed |

### 18.2 Effort estimate (on the Paperclip fork)

| Work area | Backlog items | Person-weeks |
|---|---|---|
| Trust and billing: merge service, ledger and billing center, support and status, export | S5, S1, S11, S19 | 12 |
| Verification: checker library, false-green audit, holdout runner (basic), order sizing and routing | S3, S18, S13, S12 | 13 |
| Safety and execution: sandbox images, egress, no-secrets | S4 | 5 |
| Review: evidence card and inbox | S2 | 5 |
| Start: X-ray, Product Brain, onboarding | S6, S7, S16 | 11 |
| Lines: L2, L3, L1 preview | S8, S9, S17 | 12 |
| Report and preview: weekly report, Vercel previews | S10, S14 | 6 |
| Factory UI shell | S15 | 5 |
| **Engineering subtotal (beta)** | S1–S19 | **69** |
| Design (UX and UI across modules) | — | 6 |
| Security review, red team, QA | — | 5 |
| **Total for public beta (P0)** | | **≈ 80 person-weeks** |
| **GA additions (P1)** | S20–S29, plus design and SOC 2 prep | **≈ 49 person-weeks** |

**Capacity check:** 6 engineers plus 1 designer, from mid-October to the week of 25 January, is about 15 weeks, or about **105 person-weeks**. That covers the beta P0 (about 80) with about a 25% buffer for Phase 0 concierge operations and surprises.

For comparison, the from-scratch estimate was about 145 person-weeks ([pivot proposal §6](./pivot-proposal.md#6-foundation-from-scratch-or-on-paperclip-d4)).

### 18.3 Milestones

| Milestone | Date | Exit criteria |
|---|---|---|
| **M0 Kickoff** | Early October 2026 | Team hired; fork created; Phase 0 partners recruited; SOC 2 vendor selected; Vercel and Slack app reviews planned |
| **Phase 0 readout** | Mid-November 2026 | Go/no-go gates met ([market research §8](./market-research.md#8-recommended-next-steps)) |
| **M1 Internal alpha** | End of November 2026 | L2 end-to-end on real repositories; checker library; merge service; inbox v1; sandbox red-team pass |
| **M2 Partner alpha** | Mid-December 2026 | 12 partners on L2 + L3; X-ray; evidence card; ledger in test mode; weekly report v1 |
| **M3 Private beta** | Mid-January 2027 | L1 preview; billing live; support staffed; status page; injection suite passes |
| **W0 Public beta** | Week of 25 Jan 2027 | Beta release gate (§18.4) |
| **M4** | End of March 2027 | Lights-out ladder; twins; Sentry intake; Team plan; GitLab |
| **GA** | Late April 2027 | GA release gate |

### 18.4 Release gates

| Gate | Criteria |
|---|---|
| **Public beta (W0)** | All P0 requirements for L2 and L3 pass acceptance; L1 preview passes pass^3 ≥ 85% on its golden set. Partner first-pass merge rate ≥ 60% for 2 consecutive weeks. **False green = 0** in the audit. Medium cost ≤ $6 at p50. Zero production-credential exposures; injection and reward-hacking red-team suites pass. Billing end-to-end tests pass (trial → paid → cap → pause → cancel → refund on false green). Support promise met in private beta |
| **GA** | All P1 requirements. First-pass merge rate ≥ 75%. Change-failure rate ≤ 10%. Week-4 retention ≥ 45%. Third-party penetration test with no open high findings. SOC 2 Type I report. Medium cost ≤ $5 at p50 |

---

## 19. Risks, assumptions, dependencies and open questions

### 19.1 Risks

| Risk | Impact | Likelihood | Mitigation |
|---|---|---|---|
| **Factory (factory.com) packages its Software Factory layer for small teams, Warp Factories leaves early access with small-team packaging,** or labs and platforms ship an equivalent | High | High | Outcome pricing (charge on merge, false-green refunds); safe by default; hidden holdouts; done-for-you lines; human support; benchmark on cost per verified change. Monthly competitive watch ([competitor analysis](./competitor-analysis.md)) |
| **All-in cost per Medium change is well above the modeled ≈ $5,** mainly from sandbox, CI and preview compute (Warp reports ≈ $30 per PR internally, and shows $7.07 of compute in an example; [competitor analysis §3.4](./competitor-analysis.md#34-cost-per-pr-reality-check-what-warps-numbers-mean-for-our-pricing)) | High | Medium | Phase 0 measures all-in cost by line and size on design-partner repositories. Pricing gate before beta: Medium ≤ $6 p50; at $6–10, cut Medium order size or raise its price; above $10, re-decide per-change pricing, with bring-your-own-key as the fallback (C10) |
| Reliability below target on messy repositories | High | Medium | X-ray readiness checks; "make tests runnable" orders; L2 and L3 first; order sizing |
| Outcome pricing margin squeezed by token costs | High | Medium | Routing, caching, sizing; bring-your-own-key mode; price review before GA |
| Sandbox escape or credential leak | Very high | Low | No secrets in sandboxes; egress allowlists; penetration test; red team; bug bounty after GA |
| Upstream Paperclip churn | Medium | Medium | Thin fork; weekly merges; upstream contributions |
| App-review delays (Vercel, Slack, Sentry) | Medium | Medium | Submit early; fallbacks (customer-provided preview URLs; email approvals) |
| Customer CI too slow or flaky for fast loops | Medium | Medium | Run tests in our sandbox first; flaky-test orders (L3) |

### 19.2 Assumptions

- ≥ 70% of target repositories have runnable test suites in standard images (validate in Phase 0).
- Model prices stay at or below October 2026 levels.
- Owners accept "Generated by [Brand]" labels on PRs.
- The prices in §14 cover about 90% of accounts without hitting caps.

### 19.3 Open questions (owner / due)

1. Final brand name and domain (Founder, mid-October).
2. Primary sandbox provider: E2B or Daytona (Infrastructure, week 2).
3. Default auto-run policy for L2 orders created from issues: wait for approval, or auto-run Small and Medium within the cap? (Design, Phase 0.)
4. Should the merge service ever merge without customer CI (repositories with no CI)? Current answer: no; propose a "set up CI" order first (Engineering lead).
5. Bring-your-own-key at launch for all plans, or Solo and Agency only? (Founder, by M2.)
6. Local-runner mode with personal agent subscriptions: provider terms review (Legal, before beta).
7. Holdout scenario format: Playwright scripts only, or also API checks at P0? (AI engineer, M1.)
8. Agency client access: read-only evidence cards at P1, or a client approval role? (Founder, M4.)

---

## 20. Appendices

### Appendix A: Line spec example

See [factory lines §4](./factory-lines.md#4-anatomy-of-a-line) for the full L2 Bug line spec in YAML.

### Appendix B: Core schemas (abridged)

```json
{
  "Order": {
    "id": "uuid", "issue_id": "uuid", "line": "bug|maintenance|feature|greenfield|agency",
    "size": "small|medium", "price_usd": 12, "tier": "low|medium|high",
    "state": "queued|spec|plan|build|verify|review|merging|released|done|couldnt_finish|cancelled",
    "attempts": 1, "cost_usd": 4.1, "outcome_reason": "string|null"
  },
  "EvidenceCard": {
    "order_id": "uuid",
    "checks": [{ "id": "suite_green", "tier": "L2", "pass": true }],
    "holdouts": { "passed": 3, "total": 3 },
    "scans": { "new_high": 0, "new_critical": 0 },
    "preview_url": "string|null", "pr_url": "string",
    "cost_usd": 4.1, "price_usd": 12, "model_route": ["opus-plan", "sonnet-build", "sonnet-review"]
  },
  "LedgerEntry": {
    "order_id": "uuid", "kind": "quote|charge|refund|trial_credit",
    "amount_usd": 12, "reason": "merged|false_green|trial"
  },
  "LineTrackRecord": {
    "repository_id": "uuid", "line": "maintenance", "window": "last_20",
    "first_pass_rate": 0.9, "false_green": 0, "revert_rate": 0.0, "trust_level": "ask|auto_digest"
  }
}
```

### Appendix C: Acceptance scenarios (Gherkin, key paths)

```gherkin
Feature: Charge only on merge
  Scenario: Order cannot be finished
    Given an L2 order quoted at $12
    When verification fails on 3 attempts
    Then the order state is "couldn't finish"
    And the evidence shows what was tried and a branch link
    And no ledger charge is created

Feature: Tests first
  Scenario: Reproduction must fail before the fix
    Given an L2 order for issue #231
    When the build writes a reproduction test
    Then the test is executed on the base commit
    And the order continues only if the test fails for the stated reason
    And the test file is locked during implementation

Feature: Reward-hacking guard
  Scenario: Agent tries to skip a failing test
    Given an order with a failing test in the suite
    When the build marks the test as skipped
    Then the diff policy fails the order
    And the evidence card shows "test skipped or deleted"

Feature: No production credentials
  Scenario: Sandbox environment check
    Given any order sandbox
    When the secret scanner inspects environment variables and mounted files
    Then no production credential, cloud-admin token or database URL is present

Feature: High tier is never automatic
  Scenario: Migration in a trusted line
    Given L3 maintenance is in "Auto with digest" for the repository
    When an order touches "migrations/**"
    Then the order is tiered High
    And it requires individual approval

Feature: False-green refund
  Scenario: Merged change breaks main within 7 days
    Given a merged order charged $12
    When CI on main fails due to that change on day 3
    Then the order is flagged false green
    And a $12 refund is created
    And a free L2 order is opened
    And the line is demoted one trust level

Feature: Monthly cap
  Scenario: Cap reached
    Given an account with a $300 cap and $300 charged this month
    When a new order is created
    Then it waits for approval with a message about the cap
    And no charge beyond $300 is made

Feature: Cancellation
  Scenario: Owner cancels
    Given a monthly Solo plan
    When the owner opens Billing and chooses Cancel
    Then cancellation completes in at most 2 clicks after one optional offer
    And a confirmation email states the end date and that no further charges will be made
```

### Appendix D: Notification catalog

| Notification | Channels | Timing | Respects quiet hours |
|---|---|---|---|
| Morning summary | Email, Slack, push | Owner-set time | Yes |
| High-tier change ready | Push, email, Slack | Immediately | Owner choice |
| Batch ready (Medium) | Slack, push | Owner decision windows | Yes |
| Couldn't finish | In-app, digest | Next digest | Yes |
| False green detected / rollback | Push, email | Immediately | No |
| Connection broken | Push, email | Within 15 min | No |
| Cap 80% / 100% | Email, in-app | On threshold | Yes |
| Charge in 3 days | Email | 3 days before | — |
| Incident affecting you | Email, banner | ≤ 30 min | No |
| Weekly factory report | Email, in-app | Friday (configurable) | Yes |

### Appendix E: Copy rules and key states

- **Voice:** plain, precise, calm. Use "change," "order," "line," "evidence." In the main UI, avoid "agent," "token" and "heartbeat"; those live in Advanced.
- **Never say:** "replace your engineers," "fully autonomous," "bug-free," "guaranteed," or unproven multiples.

| State | Example copy |
|---|---|
| Couldn't finish | "I couldn't reproduce bug #231 on main. I tried 3 approaches (details below). This didn't cost you anything. Want me to add logging so we can catch it next time?" |
| Evidence card | "✓ Reproduced before fix · ✓ 412 tests pass · ✓ No new security findings · ✓ Reviewed for correctness and security · Cost $4.10 · Price $12" |
| False green | "A change I merged on Tuesday broke main. I've refunded it, opened a free fix, and moved maintenance back to 'Ask me' until it earns trust again." |
| Cap reached | "You've reached your $300 cap for October. New orders will wait for your OK. Nothing will be charged beyond your cap." |
| Lights-out suggestion | "Dependency patches: 20 in a row merged without edits, 0 reverts. Let them merge automatically? You'll get a daily digest and 1 in 10 will still come to you." |

### Appendix F: Glossary

| Term | Meaning |
|---|---|
| **Line** | A packaged kind of work (Bug, Maintenance, Feature…) with stations, checks, risk rules and evals |
| **Order** | One unit of work in a line, sized Small or Medium, priced before work starts |
| **Station** | A step in the line: spec, plan, build, verify, review, release, operate, learn |
| **Definition of done** | The order's executable criteria (tests, scenarios, scans, preview, review) |
| **Holdout scenario** | An end-to-end check written at spec time and hidden from the builder |
| **Twin service** | A local fake of an external API used for testing |
| **Evidence card** | The summary of checks, cost and links shown for every change |
| **Risk tier** | Low / Medium / High; decides how a human is involved |
| **Lights-out** | A line that merges Low-tier changes automatically after earning trust |
| **False green** | A change with an all-green evidence card that fails within 7 days of merge |
| **Repo X-ray** | First-run, read-only analysis of a repository |
| **Product Brain** | The factory's editable knowledge of a repository |
| **Merge service** | The separate identity that merges approved changes |
