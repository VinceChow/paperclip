# Factory Lines: What the Factory Makes, Line by Line

**Date:** 2026-10-04 (replaces [Industry kits](../2026-09-26-opc-platform/industry-kits.md))
**Part of:** [Market research v3](./market-research.md) · [Factory harness](./reliability-cost-harness.md) · [Product feature strategy](./product-feature-strategy.md) · [PRD v2](./prd.md) · [Marketing plan](./marketing-plan.md)
**Question:** Which packaged "lines" (a kind of work plus the agents, checks and rules to do it) should the factory ship first, and what does each one need to be reliable?

---

## 1. Verdict

**Ship the factory as one product, with *lines* as the unit of onboarding, reliability, pricing and marketing.** Lines take the place the industry kits had in the OPC plan.

- **Lines solve the blank page.** A small team doesn't want to design agents. It wants "fix my bugs," "keep my dependencies current" or "build this feature." Each line arrives with:
  - its stations;
  - its definition of done;
  - default risk tiers;
  - a sandbox image;
  - an eval set.
- **Lines are the unit of trust.** Developers fully delegate only the tasks they can easily verify (0–20% of tasks today; [Anthropic](https://resources.anthropic.com/2026-agentic-coding-trends-report)). Verification difficulty therefore decides launch order. Bugs that come with a reproduction and routine maintenance are the easiest to verify, so they ship first.
- **Lines are the unit of autonomy.** Each line earns lights-out operation on its own measured track record. A line never inherits trust from another line.
- **Lines are the unit of marketing.** Each one gets a landing page, a demo and a benchmark entry ([marketing plan §4.3](./marketing-plan.md#43-line-and-audience-pages)).

## 2. Evidence that guides line choice

| Signal | Data | Implication |
|---|---|---|
| Reliable task length today | Best measured agent: about **3.1 h** of expert work at 80% success, 17.4 h at 50%; doubling about every 129 days ([METR](https://metr.org/time-horizons/)) | Each order must fit what agents finish reliably on this repository. Larger work is split |
| What engineers worry about | Review burden 24%, cost 17%, large codebases 17%, verification 15%, correctness 14% of first-person Hacker News comments ([market research §3.4](./market-research.md#34-what-they-struggle-with-today-two-voice-of-customer-sources)) | Lines must ship evidence, not just code, and must price per outcome |
| Quality of AI changes | About 1.7x more issues per PR; security pass rate 56% ([CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report), [Veracode](https://www.veracode.com/blog/2026-genai-code-security-report-ai-risk/)) | Every line runs security scans and tests written before the code |
| Destructive failures | PocketOS: production database and backups deleted in 9 seconds via an unrelated token ([Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/claude-powered-ai-coding-agent-deletes-entire-company-database-in-9-seconds-backups-zapped-after-cursor-tool-powered-by-anthropics-claude-goes-rogue)) | No line ever receives production credentials. Destructive actions are High tier |
| Checking without reading code | StrongDM: holdout scenarios outside the codebase plus cloned third-party services ([Simon Willison](https://simonwillison.net/2026/Feb/7/software-factory/)) | Lines carry holdout scenarios and use twin services for external APIs |
| Paperclip already ships a software team | `packages/teams-catalog/catalog/bundled/software-development/product-engineering` (CTO, QA and senior-coder agents; project and task templates) | The line format extends the existing teams-catalog format rather than inventing a new one |

## 3. Which lines first

Scores run from 1 (worst) to 5 (best). For *risk* and *cost*, 5 means **low** risk or **cheap** per change.

| Line | Demand | Ease of verification | Risk (5 = low) | Cost (5 = cheap) | Differentiation | Fit with first segments | **Total /30** | Release |
|---|---|---|---|---|---|---|---|---|
| **L3 Maintenance** (dependencies, security patches, flaky tests, coverage, docs) | 4 | 5 | 5 | 5 | 4 | 5 | **28** | **Beta (W0)** |
| **L2 Bug** (issue or error event → reproduction → fix) | 5 | 5 | 4 | 5 | 3 | 5 | **27** | **Beta (W0)** |
| **L1 Feature** (spec → orders → PRs → preview) | 5 | 3 | 3 | 3 | 3 | 5 | **22** | **Preview at beta; GA** |
| **L5 Agency client** (client workspaces, handovers, per-client reports) | 4 | 3 | 3 | 3 | 5 | 4 | **22** | **GA** |
| **L4 Greenfield SaaS** (spec → new app on a standard blueprint → deployed) | 4 | 3 | 4 | 2 | 4 | 4 | **21** | **GA** |
| L6 API and integrations | 3 | 4 | 3 | 4 | 2 | 3 | 19 | After GA |
| L7 Mobile (Expo / React Native) | 3 | 2 | 3 | 2 | 3 | 3 | 16 | Later |
| L8 Data pipelines | 3 | 3 | 3 | 3 | 2 | 2 | 16 | Later |
| L9 Legacy modernization | 4 | 3 | 2 | 2 | 4 | 1 | 16 | Enterprise wedge (Phase 3) |

The scores are judgment calls based on the evidence above. Phase 0 will re-score them using measured first-pass merge rates per line (§8).

**Beta scope (W0, week of 25 Jan 2027):** L2 and L3 generally available in beta; L1 in preview, for features up to Medium size on TypeScript or Python web apps.
**GA (late April 2027):** L1 fully available, plus L4 and L5.

## 4. Anatomy of a line

A line is a versioned package that extends Paperclip's teams-catalog format (`TEAM.md`, agents, projects, tasks). It has eight parts:

| Part | What it contains | Paperclip mapping |
|---|---|---|
| **Intake** | What starts an order: issue labels, error-tracker events, schedules, specs, voice notes | Issues, routines, connections, webhooks |
| **Stations** | Spec → plan → build → verify → review → release → operate → learn, with the agent role and model tier per station | Agents/skills in the teams catalog; adapters; `issue_plan_decompositions` |
| **Definition of done** | Executable criteria: tests, holdout scenarios, scans, preview health, size limits | `completion_contracts` and `work_assessments`, extended with code checkers ([harness §4](./reliability-cost-harness.md#4-the-factory-loop)) |
| **Risk rules** | Change tier per file path and type; branch protections; merge policy | Approvals, GitHub review checks, issue review policy |
| **Sandbox image** | Language runtimes, package caches, test tools, twin services | Sandbox providers (Daytona, E2B, Modal and others); execution workspaces |
| **Budgets** | Per-order cost cap, per-month cap, time limits | Budget policies and incidents; cost events |
| **Evals** | 20–50 golden tasks per line with holdout scenarios; pass^3 target; false-green audit | Runner evals and product end-to-end evals |
| **Report** | Metrics the line contributes to the weekly factory report | Activity log, cost events, work products |

Every line is described in a spec like this:

```yaml
line: bug
version: 1.0.0
intake:
  - { event: issue.labeled, label: bug }
  - { event: error_tracker.new_issue, min_events: 5 }     # e.g. Sentry
stations:
  triage:   { model_tier: small,  output: [severity, area, reproducible?] }
  reproduce:{ model_tier: mid,    output: failing_test }   # must fail on main before any fix
  fix:      { model_tier: mid,    escalate_to: frontier, after_failures: 1 }
  verify:   { checks: [failing_test_now_passes, full_suite_green, typecheck, lint,
                       sast_clean, secrets_clean, diff_size_lte_400_lines] }
  review:   { agents: [correctness, security], post_as: github_review }
definition_of_done:
  required: [reproduction_test_added, reproduction_failed_before_fix, suite_green,
             no_new_high_findings, evidence_card_complete]
risk:
  default_tier: medium
  high_paths: ["migrations/**", "**/auth/**", "**/billing/**", "infra/**", ".github/workflows/**"]
budget: { per_order_usd: 8, max_attempts: 3 }
lights_out:
  eligible_tiers: [low]
  promote_after: { consecutive_merges_without_edit: 20, false_green: 0, revert_rate_lte: 0.02 }
evals: { golden_tasks: 40, target_pass_k3: 0.85 }
pricing: { small: 3, medium: 12 }   # USD per merged change; failed orders free
```

## 5. Lines in detail

### 5.1 L2 Bug line ("Bugs fixed with proof")
**For:** everyone. It is the first line most accounts turn on.
**Intake:** issues labeled `bug`; error-tracker issues above a threshold; support tickets that are forwarded.

| Station | What happens | Done means |
|---|---|---|
| Triage | Classify severity and area; check whether it can be reproduced | Labels set; duplicate check done |
| Reproduce | Write a test that fails on `main` | The test fails for the stated reason (asserted) |
| Fix | Minimal change; one escalation to a frontier model after the first failure | The reproduction test passes |
| Verify | Full suite, typecheck, lint, SAST, secret scan, diff-size limit | All green; evidence card complete |
| Review | Correctness and security review agents post a GitHub review; the risk tier decides who approves | Medium: batch approval. High paths: individual approval |
| Release | Merge behind the repository's normal pipeline | CI green after merge |

- **Can't reproduce:** the order ends as "couldn't reproduce" with what was tried. It is **free**.
- **Lights-out candidates:** Low-tier fixes, meaning test-only or copy changes.
- **Metrics:** reproduction rate, first-pass merge rate, regressions within 14 days.

### 5.2 L3 Maintenance line ("Keep it current while you sleep")
**For:** solo founders and agencies with many repositories. This is the first line expected to go lights-out.

| Job | Trigger | Done means | Default tier |
|---|---|---|---|
| Dependency patch and minor upgrades | Weekly; advisories | Lockfile updated; full suite green; changelog summary; no new scan findings | Low (patch) / Medium (minor) |
| Major upgrades | On request | Migration steps applied; suite green; preview healthy | High |
| Security advisories | New advisory affecting the repository | Fixed version or mitigation; proof the vulnerable path is gone (scan) | Medium |
| Flaky tests | Repeated CI flakes | Root cause fixed (not retried or skipped); 20 consecutive green runs | Low |
| Coverage | Monthly; files below target | New tests that fail when the code is mutated (mutation check on the changed lines) | Low |
| Docs drift | Merged PRs that change the public API | README and API docs updated; links valid | Low |

**Never:**
- disable or skip a test to get green;
- loosen a lint rule;
- pin a vulnerable version.

### 5.3 L1 Feature line ("Specs in, features out")
**For:** solo founders and small teams shipping a roadmap.

| Station | What happens | Done means |
|---|---|---|
| Spec | Owner writes or dictates the need; the factory drafts a spec with acceptance checks and holdout scenarios (stored outside the repository) | **Owner approves the spec** (always, at launch) |
| Plan | Split into orders sized to the repository's measured success rate; dependencies set | Each order is Small or Medium; the plan shows a price before any build |
| Build | Tests first, then code, in a sandbox, behind a feature flag | Order checks pass |
| Verify | Unit and integration tests, holdout scenarios against a preview environment, scans, twin services for external APIs | All required checks pass; preview is healthy |
| Review | Evidence-first inbox; the risk tier decides | Approved |
| Release | Flag on for the owner first, then staged rollout | Health checks pass; rollback is ready |

- **Preview scope at beta:** TypeScript (Next.js, Node) and Python (FastAPI, Django) web apps; features up to Medium size.
- **Metrics:** spec-to-merge cycle time, first-pass merge rate, false-green rate, change-failure rate.

### 5.4 L4 Greenfield SaaS line ("A production-grade v1, not a prototype")
**For:** solo founders starting something new, and agencies doing new client builds.

- **Blueprint:**
  - Next.js and TypeScript, Postgres, authentication, Stripe billing;
  - transactional email, error tracking, CI;
  - preview environments, infrastructure as code;
  - row-level security on by default.
- **Done means:**
  - the spec's holdout scenarios pass on a deployed preview;
  - scans are clean;
  - there are no secrets in the repository;
  - authorization tests cover every data table.
- **Answers the app-builder failure pattern:** apps that leak data or can't be maintained ([CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/)).
- **Handover:** a normal Git repository the customer owns, with docs and runbooks. No lock-in.

### 5.5 L5 Agency client line ("Your studio, multiplied")
**For:** agencies and freelancers.

- **Client workspaces:** separate repositories, secrets, budgets and reports per client.
- **Per-client cost report:** cost per change and margin per project.
- **Handover pack:** architecture notes, runbooks, test map, change log with evidence.
- **Client-facing evidence:** share a read-only evidence card or weekly report with the client (optional).

## 6. Risk tiers and the lights-out ladder (common to all lines)

| Tier | Types of change | Default handling | Can go lights-out? |
|---|---|---|---|
| **Low** | Docs, tests, refactors fully covered by tests, dependency patch versions, lint fixes | Automatic merge once the line is trusted | **Yes**, per line, on evidence |
| **Medium** | Features behind flags, minor upgrades, UI changes, bug fixes outside high-risk paths | Batch approval in the inbox | After GA, per repository, on evidence |
| **High** | Schema migrations, authentication, payments, permissions, infrastructure, CI configuration, deleting data, anything touching production secrets | Individual approval, every time | **Never** in v1 |

**Lights-out ladder:**
1. **Draft only:** PR opened, nothing merged.
2. **Ask me:** inbox approval.
3. **Auto with digest:** merge automatically and summarize daily. Requires all of the following for that line and repository:
   - ≥ 20 consecutive merges without edits;
   - zero false-green;
   - revert rate ≤ 2%;
   - no High-path changes.
4. **One in ten is sampled** into the inbox for spot checks.

Any revert or post-merge failure drops the line one step automatically.

## 7. Open line format and public factory benchmark (replaces the kit marketplace)

- **Open line format:**
  - the YAML spec in §4, plus line packages in the teams-catalog layout;
  - license: MIT;
  - anyone can publish community lines (for example Rails upgrades or a Django admin line).
  
  Listing requirements for community lines:
  - an eval set;
  - published pass^3 and false-green rates;
  - no production-credential requirements.
- **Public factory benchmark,** published quarterly:
  - real tasks from consenting open-source repositories, with holdout scenarios;
  - reported per line: first-pass merge rate, pass^3, false-green rate, **cost per verified change**, and wall-clock time;
  - runs every major model and agent adapter Paperclip supports, so the benchmark is model-neutral by design.
- **Why it matters:**
  - category creation ("what does a verified change cost?");
  - PR (the State of AI Software Factories report);
  - a community flywheel;
  - and it keeps us honest.

## 8. What to validate in Phase 0

- [ ] Measured first-pass merge rate, false-green rate and cost per change for **L2 and L3** on the 12 design-partner repositories. Re-score §3.
- [ ] Which maintenance jobs partners will allow lights-out after 4 weeks (the expected answer is patch upgrades, flaky tests and docs).
- [ ] Whether partners will write or approve specs with holdout scenarios for L1 (time per spec, and willingness).
- [ ] Agency interest in L5 at the Agency plan price ($399 a month plus changes).
- [ ] Sandbox image coverage: the share of partner repositories whose test suite runs in our standard images without custom setup (target ≥ 70%).
