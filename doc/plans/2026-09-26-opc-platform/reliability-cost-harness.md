# Reliability and Cost: The Outcome Loop Harness for One-Person Companies

**Date:** 2026-09-26
**Part of:** [Market Research Report (v2)](./market-research.md) · [Industry kits](./industry-kits.md) · [Marketing plan](./marketing-plan.md)
**Question:** How do we make sure agents *get the requested job done as instructed*, with results users can rely on, at a reasonable cost? What harness and loop engineering does that take, and how much of it does Paperclip already have?

---

## 1. Summary

- **Agents fail in predictable ways.** Anthropic's own long-running harness work names two failure modes:
  - *Overambition*: trying to do everything at once and leaving work half-done.
  - *Premature completion*: declaring the job done without verifying it.

  Consistency is also weaker than one-off success: on τ-bench, the best model's pass^8 was about 60% below its pass^1. The answer is a **harness**, not a better prompt.
- **The design: an "outcome loop."** Every job carries an **outcome contract** (a definition of done). A doer and a separate checker work the job in small steps. Deterministic checks run before model judgment, and a human approves anything irreversible. Retries escalate effort, and each run has a hard budget. Every user correction becomes an eval case.
- **Cost stays reasonable when you choose workflows over always-on agents and use routing plus caching.** Our model at current Claude list prices:
  - About **$31–$39** of inference per active user per month.
  - About **$114** for the same work on a single frontier model without caching.
  - About **$980** for an org chart of 5 agents on 30-minute heartbeats.
- **Paperclip already has much of the machinery:** budgets with hard stops, approvals, native completion reviews, a task watchdog, recovery with a three-attempt budget, monitors, low-trust presets, and evals. The missing pieces are the outcome contract, a checker library, rubric graders, model routing and cache discipline, per-kit evals, and a cost-per-accepted-deliverable metric.

## 2. Why agents don't finish jobs (evidence)

| Failure | Evidence | Harness response |
|---|---|---|
| Overambition: does too much, runs out of context mid-task | Anthropic: agents left "a feature half-implemented and undocumented"; fixed by working "on only one feature at a time" ([Anthropic, long-running harnesses](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)) | Small steps; a checklist in a progress document |
| Premature completion: "looks done" | Later sessions "declare the job done"; features marked complete "without proper testing" (same source) | Outcome contract with every criterion marked *failing* until verified; an independent checker |
| Inconsistency across runs | τ-bench (2024 models): best model <50% pass^1, **~25% pass^8** in retail ([Sierra](https://sierra.ai/blog/benchmarking-ai-agents)). Newer models score higher, but the gap between pass^1 and pass^k persists as a pattern. | Measure pass^k; narrow scopes; deterministic steps where possible |
| Long, realistic office work is hard | TheAgentCompany: best agent completed **~30%** of 175 office tasks (2025-era models) ([paper](https://papers.nips.cc/paper_files/paper/2025/file/0d744742f6fac4d1134c019b7cef3c8a-Paper-Datasets_and_Benchmarks_Track.pdf)) | Workflows with defined steps instead of open-ended autonomy |
| Capability is rising fast | METR: the 50% time horizon is doubling every ~4–7 months ([METR](https://metr.org/time-horizons/)) | Design so that model upgrades improve results without redesign |
| Multi-agent coordination is expensive | Agents use **~4x** the tokens of chat; multi-agent systems **~15x** ([Anthropic, multi-agent research](https://www.anthropic.com/engineering/multi-agent-research-system)) | One orchestrator plus skills; subagents only for parallel research |
| Environment is illegible | OpenAI's "harness engineering": the bottleneck is environment legibility; `AGENTS.md` works best as a table of contents; struggles are treated as signals that something is missing from the environment ([OpenAI](https://openai.com/index/harness-engineering/)) | The business profile plus kit docs act as the agent's source of truth |
| Destructive or unwanted actions | The Replit agent deleted a production database during a code freeze ([AIID #1152](https://incidentdatabase.ai/cite/1152/)); OpenClaw's security incidents | Approvals enforced in code; least-privilege scopes; idempotent delivery |

## 3. Design principles

1. **Workflows first, agents where needed.** Use predefined code paths (chaining, routing, parallelization) for recurring jobs. Reserve open-ended agent loops for research and planning. "Agentic systems often trade latency and cost for better task performance" ([Anthropic, building effective agents](https://www.anthropic.com/engineering/building-effective-agents)).
2. **Every job has an outcome contract.** It states what "done" means as 5–10 independently checkable criteria, plus inputs, tools, the approval point and the budget. This mirrors Anthropic's feature list, where every item starts as failing, and its Managed Agents *outcomes* (a rubric plus a separate grader that iterates until satisfied).
3. **Separate the doer from the checker.** Use the evaluator-optimizer pattern. The grader runs in an independent context against the rubric. Paperclip's native completion review already has reviewer agents that accept or reject.
4. **Check cheaply first.** Run code-based checks before model graders. They are "fast, cheap, objective, reproducible" ([Anthropic, evals](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)). This matches the "backpressure" idea in the Ralph loop, where tests and type checks gate each iteration ([ghuntley](https://ghuntley.com/ralph/)).
5. **Small steps, external memory.** One deliverable per iteration. Keep a progress checklist in the task document and repeat the plan near the end of the context ("todo.md recitation"). Keep errors in context so the agent learns from them ([Manus](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus)).
6. **Humans at the boundary.** Anything outward-facing or irreversible (send, post, pay, delete) requires approval by default. Autonomy is earned per action type (the trust ladder).
7. **Event-driven, not timer-driven.** Wake on a new email, a new lead or a finished meeting. Use low-frequency schedules only for briefs and reports.
8. **Cost is a first-class service-level objective.** Measure *cost per accepted deliverable* (p50/p90), not cost per call. Enforce hard dollar caps per job and per month.
9. **Learn from every correction.** Each user edit or rejection becomes a golden-task candidate. Start with 20–50 real tasks. Keep capability evals (low pass rate) separate from regression evals (~100% pass). Read transcripts.
10. **Honest failure beats fake success.** When the contract can't be met within budget, say what's missing, and never mark the job done.

## 4. The Outcome Loop

```
 trigger (event / schedule / user ask)
        │
        ▼
 ┌─────────────┐   fills contract from kit + business profile
 │   INTAKE    │── missing input? ──► ask user (durable question) ──┐
 └─────┬───────┘                                                    │
       ▼                                                            │
 ┌─────────────┐   checklist of small steps written to task doc     │
 │    PLAN     │                                                    │
 └─────┬───────┘                                                    │
       ▼                                                            │
 ┌─────────────┐   routed model, low/medium effort, cached prefix   │
 │     DO      │◄────────────────────────────┐                      │
 └─────┬───────┘                             │ revise (≤ N)         │
       ▼                                     │ escalate effort/model│
 ┌─────────────┐  L1 deterministic checks    │ on 2nd failure       │
 │    CHECK    │  L2 rubric grader (indep.)  ├──────────────────────┘
 │             │  L3 source / fact checks    │
 └─────┬───────┘── fail ─────────────────────┘
       │ pass                                   budget or attempts exhausted
       ▼                                        ──► "couldn't finish: <reason>" + partial work
 ┌─────────────┐   trust ladder decides: ask human / auto
 │   APPROVE   │── rejected / edited ──► edit captured as eval case ──► DO
 └─────┬───────┘
       ▼
 ┌─────────────┐   idempotent side effects (send, post, invoice)
 │   DELIVER   │
 └─────┬───────┘
       ▼
 ┌─────────────┐   did it actually happen? (sent, scheduled, created)
 │   VERIFY    │   monitor for follow-ups (reply? paid?)
 └─────┬───────┘
       ▼
 ┌─────────────┐   results + cost + what didn't work → weekly report
 │ REPORT/LEARN│
 └─────────────┘
```

### 4.1 Outcome contract (schema sketch)

```yaml
outcome_contract:
  job: proposal_from_discovery_call
  deliverable: proposal_draft.docx
  inputs_required: [meeting_transcript, rate_card, business_profile]
  criteria:                        # all start as "failing"
    - id: goals_covered      check: grader     rule: "every goal stated by client in transcript is addressed"
    - id: pricing_matches    check: code       rule: "prices == rate_card options (±0)"
    - id: sections_present   check: code       rule: "scope, timeline, 3 options, next steps"
    - id: no_hallucinated_refs check: grader   rule: "no case studies or clients not in profile"
    - id: voice              check: grader     rule: "voice score >= 4/5 vs samples"
    - id: length             check: code       rule: "<= 4 pages"
  approval: always                 # outward-facing
  budget: { usd_hard_cap: 1.50, max_attempts: 3, max_revisions: 2 }
  on_fail: report_gap_and_partial
```

### 4.2 Verification tiers by job type

| Job type | L1 deterministic checks | L2 grader (rubric) | L3 external verification | Default approval |
|---|---|---|---|---|
| Emails and replies | Recipient in thread or CRM; no placeholder text; links resolve; no attachment mismatch; tone/ban list | Answers the question; accurate to thread; voice | Delivery receipt | Ask first → auto after a track record |
| Social and content | Length, hashtags, duplicate vs history, banned claims, #ad present when sponsored | One idea, CTA, voice, factual claims cited | Published URL exists | Ask first |
| Proposals and invoices | Totals equal the rate card or contract; required sections; dates valid | Client goals covered; no invented references | PDF renders; invoice ID created | Always |
| Research (leads, market) | Source URLs present and fetchable; dedupe; schema-valid fields | Relevance to the ideal client profile; citation accuracy (claims match sources) | Spot re-fetch of 10% | None (internal) |
| Calendar and admin | No conflicts; time zone correct; attendees valid | — | Event exists | Auto |
| Real estate outbound | TCPA consent flag; quiet hours; Fair Housing phrase checker | Factual match to the MLS listing | Opt-out handling | Always (Phase 2) |

### 4.3 Retry and escalation policy (measured basis)

- **First attempt** runs on the routed model at **low or medium effort**.
- **On a check failure**, revise with the failed criteria as feedback (up to `max_revisions`).
- **On a second failure**, escalate effort or the model tier once. Anthropic measured this "re-run failures at higher effort" policy on SWE-bench Pro with Claude Opus 5.5: about **97% pass at ~45% lower cost** than running everything at high effort ([Anthropic cost guidance](https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence.md)).
- **Cap attempts at 3.** This matches Paperclip's existing shared incident budget of three provider attempts (`doc/plans/2026-09-08-reliable-execution-recovery.md`). After that, report honestly with the partial work.
- **The watchdog** restarts trees that stopped for the wrong reason, such as a misread blocker or "done" without proof (`doc/TASK-WATCHDOG.md`).

## 5. Measuring reliability ("result-driven" as numbers)

| Metric | Definition | MVP target |
|---|---|---|
| **Contract completion rate** | Jobs where every criterion passed, divided by jobs started | ≥ 90% on Phase 1 workflows |
| **First-pass acceptance** | Deliverables approved by the user with no edits, divided by deliverables presented | ≥ 60% at launch → ≥ 80% by month 3 |
| **Accepted-with-light-edit** | Approved with an edit distance under 15% | Tracked |
| **pass^3 on golden tasks** | All 3 repeated runs pass the contract | ≥ 85% per workflow before a kit ships |
| **Honest-failure rate** | "Couldn't finish" reports, divided by jobs | < 5%, with zero *false* "done" |
| **Cost per accepted deliverable** | $ spent (including retries and grading) divided by accepted deliverables, p50/p90 | Routine jobs < $0.25 p50; long-form < $1.00 p50 |
| **Time to done** | Trigger → delivered | Per workflow, SLO shown to user |
| **Business KPIs** | Per kit: follow-ups sent, proposals out, posts published, receivable days | Shown in weekly report |

**Eval program**
- For each workflow, 20–50 golden tasks built from real pilot jobs.
- Code graders run first, then a model grader calibrated against human labels.
- *Capability* suites (hard, low pass rate) are kept separate from *regression* suites (~100%).
- Run pass^k on every kit or model change.
- Watch "price the tail": in one run, **2 of 20 problems carried 43% of the spend**.

## 6. Cost engineering

### 6.1 Prices used (Claude API list, 2026-09-26)

| Model | Input / Output per MTok | Cache read | Best use in OPC |
|---|---|---|---|
| Claude Haiku 4.5 | $1 / $5 | $0.10 | Classification, routing, L2 grading of simple rubrics, extraction |
| Claude Sonnet 5 | $2 / $10 | $0.20 | Most drafting, replies, lead research |
| Claude Opus 5.5 | $4 / $20 | $0.20 (0.05x) | Long-form content, proposals, weekly strategy, hard revisions |
| Claude Fable 5.1 | $10 / $50 | $0.25 (0.025x) | Rare; deep research only |

Other pricing that matters:
- 5-minute cache writes cost 1.25x input; 1-hour writes cost 2x.
- Batch is 50% off (it stacks with caching).
- Web search is $10 per 1,000 searches.
- Managed Agents session runtime is $0.08 per session-hour ([pricing](https://platform.claude.com/docs/en/about-claude/pricing)).

### 6.2 Levers ranked, with measured effects (Anthropic)

| Lever | Measured effect | Apply in OPC |
|---|---|---|
| **Prompt caching** | **2.7x–5.3x** cheaper agent loops at 79–90% hit rates; a triage agent 83–88% cheaper | Stable prefix: system prompt → tool list → business profile → kit docs; volatile data after the breakpoint; verify `cache_read_input_tokens` |
| **Model routing** (cost per *solved* task, not per token) | Opus 5.5 at medium: **92.8% solved at $0.22 per solved task**, beating Fable 5.1 at default ($1.19); Haiku ~1/5 of Opus 5.5 cost on GPQA at 63% vs 92% | Haiku for checkable high-volume work; Sonnet 5 or Opus 5.5 at medium for drafting; measure per workflow |
| **Effort tuning** | Knowledge work: medium matched default accuracy at **70–87% of the cost**; low cost 1–3 points for 33–50% savings | Default medium; low for classification and grading |
| **Re-run failures at higher effort** | ~97% pass for ~45% less cost | Built into §4.3 |
| **Batch API** | 50% off all tokens | Nightly research, weekly reports, eval runs |
| **Task budgets** | Generous budget: −44% cost for ~3 points | Per-job caps from the p90 of observed usage |
| **Output shape** | One-line vs memo final answers: memo cost **2.8x** at the same accuracy | Strict output schemas per deliverable |
| **Files + code execution for data** | A 1,862-row CSV pasted in the prompt: 6/25 correct, $5.01; uploaded plus code execution: **25/25, $0.40** | Spreadsheets and reports go through code execution |
| **Tool search / narrow tools** | With 502 tools, cost stayed flat (~$0.56) instead of rising to $1.02 | Load only the kit's tools |
| **Prompt audit** | Unaudited prompts **36% more expensive**; audited, 14% cheaper and more accurate | Re-audit kit prompts on every model migration |
| **Don't under-cap `max_tokens`** | A 16K cap cut off 25–43% of attempts, and almost none of the cut-off attempts passed | 64K for agentic runs, with streaming |

Source for every row: [Anthropic, optimizing for cost and intelligence](https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence.md). These are Anthropic's benchmarks; re-measure on OPC workloads.

### 6.3 Per-user model (assumptions stated)

Workload for one active OPC user per month. Prices are list prices; with caching, each turn reads the prior context from the cache and writes only new tokens.

| Job | Count / mo | Model | $/job | $/mo |
|---|---|---|---|---|
| Daily brief | 30 | Sonnet 5 | 0.045 | 1.34 |
| Inbox triage (classify) | 900 | Haiku 4.5 | 0.004 | 3.49 |
| Reply drafts | 150 | Sonnet 5 | 0.027 | 4.11 |
| Long-form content (agentic, ~12 turns) | 13 | Opus 5.5 | 0.60 | 7.83 |
| Lead research (web, ~6 turns, 3 searches) | 80 | Sonnet 5 | 0.147 | 11.76 |
| Weekly report | 4 | Opus 5.5 | 0.40 | 1.60 |
| Rubric grader passes | 260 | Haiku 4.5 | 0.004 | 1.14 |
| **Total (routed + cached + event-driven)** | | | | **≈ $31** (≈ $39 with 25% for revisions and retries) |

| Alternative design for the same work | $/mo |
|---|---|
| Routed, **no caching** | ≈ $69 |
| Everything on Opus 5.5, no caching | ≈ $114 |
| Org chart: 5 agents on **3-hour heartbeats** (2 turns × 30K context, no cache hits) | ≈ $163 |
| Org chart: 5 agents on **30-minute heartbeats** | ≈ **$980** |

**Takeaways:**
- The org-chart-with-heartbeats pattern that Paperclip users run into (Reddit reports of "surprise token bills") is the biggest cost risk. Show a *team* in the UI, but run *event-triggered workflows* underneath.
- Caching roughly halves cost again once models are routed.
- Lead research dominates cost, so gate it (for example 20 leads a week on the Solo plan).

### 6.4 Budget enforcement (layers)

1. **Per job:** a dollar hard cap in the outcome contract, plus an advisory task budget for the model.
2. **Per workflow per day:** a rate limit (for example, lead research at most 25/day).
3. **Per company per month:** a plan allowance shown in dollars and jobs. When it's exhausted, the company auto-pauses (Paperclip's budget hard-stop invariant) and the user is notified.
4. **Platform:** workspace spend limits as the final backstop.

## 7. Paperclip today: what exists vs what to build

| Capability needed | Exists in this repo | Gap / change for OPC |
|---|---|---|
| Budgets and auto-pause | ✅ Budget hard-stop invariant (`AGENTS.md` §5) | Show in dollars and jobs; add per-job caps inside contracts |
| Human approvals | ✅ "Ask human / Ask first" tool-action reviews with signed arguments (`doc/connections/TASK-REVIEWS.md`) | **Trust ladder**: per-action autonomy levels; suggest promotion after N unedited approvals |
| Doer and checker separation | ✅ Native completion reviews: reviewer accepts or rejects; a review run with no decision can't mark Done (`doc/execution-semantics.md`) | Make a **rubric grader** the default reviewer for every kit deliverable (cheap model, independent context) |
| Restart wrongly stopped work | ✅ Task watchdog (`doc/TASK-WATCHDOG.md`) | Enable by default on kit workflow roots |
| Recovery and retries | ✅ Three-attempt incident budget; continuation envelopes (`doc/plans/2026-09-08-reliable-execution-recovery.md`) | Add **effort/model escalation** on retry; honest-failure report |
| Follow-up checks | ✅ One-shot monitors (`executionPolicy.monitor`) | Use for "did they reply?" and "was the invoice paid?" |
| Durable questions to the user | ✅ Durable interactions before waiting | Use for missing contract inputs at intake |
| Untrusted inbound content | ✅ `low_trust_review` preset (`doc/LOW-TRUST-PRESETS.md`) | Apply to inbox, web and DM content (prompt-injection defense) |
| Evals | ✅ Runner Evals and Product E2E Evals (`doc/evals.md`) | **Per-kit outcome evals**: golden tasks, pass^k, cost per accepted deliverable |
| Outputs | ✅ Work products and artifacts | Results gallery for non-technical users |
| Templates | ◐ Teams catalog and ClipHub concept | **Kits** with outcome contracts, guardrails, seed tasks, evals |
| Cost tracking | ◐ Per-agent spend; $0 for subscription-billed agents ([#339](https://github.com/paperclipai/paperclip/issues/339)) | Hosted API billing; cache-hit and cost-per-accepted-deliverable metrics |
| **Outcome contract** | ❌ | New object on issues/routines: criteria, checks, approval, budget |
| **Deterministic checker library** | ❌ | Links, totals, lengths, banned phrases, recipients, calendar conflicts, TCPA, Fair Housing, #ad |
| **Model router + cache discipline** | ❌ (adapter per agent) | Per-step model and effort; stable-prefix prompt assembly; cache diagnostics |
| **Event triggers from connections** | ◐ (routines, wakes) | Gmail, calendar and form webhooks → workflow triggers instead of heartbeats |

**Execution-layer options**
- **(a) Paperclip Runner with direct API calls.** Model-agnostic and fully under our control.
- **(b) Anthropic Managed Agents per job.** It provides a hosted loop, *outcomes* (rubric + grader iterations, up to 20), **session budgets as hard dollar caps**, and permission policies (`always_ask` / `auto`) at $0.08 per session-hour.

Option (b) speeds up the pilot; option (a) avoids lock-in. Recommendation: prototype the outcome loop in Paperclip, and keep the contract format portable so either layer can execute it.

## 8. Build list (priority order)

1. Outcome contract object and UI ("definition of done" shown on every job).
2. Checker library (L1), plus rubric grader as the default completion reviewer (L2).
3. Model router with effort defaults, stable-prefix prompt assembly, and cache-hit telemetry.
4. Trust ladder built on the existing approvals.
5. Event triggers from Gmail and Calendar; retire tight heartbeats for kits.
6. Metrics: contract completion, first-pass acceptance, pass^k, cost per accepted deliverable. These feed the weekly report.
7. Per-kit eval suites and an "edit → eval case" pipeline.
8. Honest-failure UX and effort escalation on retry.

## Sources

- Anthropic engineering: [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) · [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) · [Multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system) · [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- Anthropic docs: [Pricing](https://platform.claude.com/docs/en/about-claude/pricing) · [Optimizing for cost and intelligence](https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence.md) · [Managed Agents outcomes](https://platform.claude.com/docs/en/managed-agents/define-outcomes.md) · [Permission policies](https://platform.claude.com/docs/en/managed-agents/permission-policies.md)
- [OpenAI: Harness engineering](https://openai.com/index/harness-engineering/) · [Manus: Context engineering lessons](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) · [Geoffrey Huntley: Ralph](https://ghuntley.com/ralph/)
- [Sierra: τ-bench and pass^k](https://sierra.ai/blog/benchmarking-ai-agents) · [METR time horizons](https://metr.org/time-horizons/) · [TheAgentCompany](https://papers.nips.cc/paper_files/paper/2025/file/0d744742f6fac4d1134c019b7cef3c8a-Paper-Datasets_and_Benchmarks_Track.pdf) · [AI Incident Database #1152](https://incidentdatabase.ai/cite/1152/)
- This repo: `doc/execution-semantics.md`, `doc/TASK-WATCHDOG.md`, `doc/connections/TASK-REVIEWS.md`, `doc/plans/2026-09-08-reliable-execution-recovery.md`, `doc/LOW-TRUST-PRESETS.md`, `doc/evals.md`, `doc/CLIPHUB.md`
