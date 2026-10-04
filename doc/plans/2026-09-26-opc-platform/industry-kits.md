# Industry Kits for One-Person Companies: Demand Research and Kit Design

> **Superseded (2026-10-04).** The product pivoted to an AI software factory. This document is kept for history. The current version is [../2026-10-04-software-factory/factory-lines.md](../2026-10-04-software-factory/factory-lines.md); see the [pivot proposal](../2026-10-04-software-factory/pivot-proposal.md) for why.


**Date:** 2026-09-26
**Part of:** [Market Research Report (v2)](./market-research.md) · [Reliability and cost harness](./reliability-cost-harness.md) · [Marketing plan](./marketing-plan.md) · [Product feature strategy](./product-feature-strategy.md) · [PRD](./prd.md)
**Question:** Does it help to ship ready-made *industry kits* (templates of agents, workflows and orchestration) for the major one-person-company industries: consultants, coaches, designers, property agents, creators, and others?

---

## 1. Verdict

**Yes. Kits should be the main way users onboard and the main way the product is marketed, but they belong inside one horizontal product.** Don't build separate vertical products.

- **Kits solve the blank-page problem that kills activation for non-technical users.** Users get a working "company" on day one: a team, recurring jobs and a first week of wins. They don't have to design agents.
- **Per-industry search demand is real but thin.** In US Google Trends (12-month mean, same scale), "AI for small business" scores **48**. Industry terms score far lower: consultants 6.8, designers 5.4, real estate agents 5.1, coaches 4.5, content creators 4.1, therapists 3.4, photographers 2.2. So one brand should be the demand magnet, with industry landing pages and kits capturing the long tail.
- **Kits are the unit of reliability.** Each kit is a small set of well-defined recurring workflows. Each workflow has an *outcome contract* and a golden-task eval suite, which is what makes "result-driven" achievable (see the [harness document](./reliability-cost-harness.md)). Open-ended "do anything" agents cannot be verified at this level.

## 2. Evidence that templates drive adoption

| Signal | Data | Source |
|---|---|---|
| Community appetite for ready-made workflows | n8n's official library has **11,741 workflows (Aug 2026), 69% AI**, up from ~8.3K in early 2026 | [n8n workflows](https://n8n.io/workflows/), [ConnectSafely](https://connectsafely.ai/articles/n8n-templates-workflow-automation-examples) |
| Creation is cheap; curation is scarce | **3M+ custom GPTs** created, only a small share listed in the GPT Store (~159K listed per one analysis) | [seo.ai](https://seo.ai/blog/gpt-store-statistics-facts) |
| Templates as a growth loop | Notion's role-specific starter templates removed blank-page paralysis and became a viral acquisition loop | [ProductLed](https://productled.com/blog/activation-rate-saas) |
| Activation drives retention | +25% activation → +34.3% monthly retention after a year (Appcues); each 10-minute cut in time-to-first-value → +8–12% activation (Product Led Institute) | Via [ProductLed](https://productled.com/blog/activation-rate-saas) (secondary) |
| Competitors already sell "use cases" and templates | Sintra "Use Cases" (one-click work); PaperclipCloud "pre-built AI company templates: content agencies, support teams, e-commerce operators"; Taskade Genesis community gallery | [Sintra](https://sintra.ai/pricing), [PaperclipCloud](https://paperclipcloud.com/), [Taskade](https://www.taskade.com/blog/one-person-companies) |
| Vertical willingness to pay is proven | Lofty "Agentic OS" for real estate at **$299/mo** for solo agents; coach AI clones **$99/mo + 10–15%** revenue share | [Ascendix](https://ascendix.com/blog/ai-real-estate-agents/), [Personify](https://personify.fyi/blog/ai-clone-cost/) |
| Industries already use generic AI and want time back | Realtors: 48% use AI daily or weekly; 91% of AI users use ChatGPT; **81% adopt tech mainly to save time** | [NAR 2026](https://www.nar.realtor/newsroom/realtors-adopt-technology-to-save-time-and-improve-the-client-experience-nar-report-finds) |
| Adoption gap in coaching | 54% of coaches call tech platforms a priority; **only 6%** use AI coaching tools | [ICF 2025](https://coachingfederation.org/blog/coaching-industry-continues-global-growth-with-5-34-billion-usd-revenue-new-research-reveals/) |
| Paperclip already has the building blocks | `packages/teams-catalog` (bundled: company-defaults, product, software-development; optional: content) and the ClipHub "download a company" concept (`doc/CLIPHUB.md`). No kits exist yet for service businesses. | This repo |

**Implication:** Generic ChatGPT is already in these users' hands. A kit wins only if it runs the *whole workflow*: trigger, draft, check, approve, send, follow up, report. Better prompts alone won't beat ChatGPT.

## 3. Which industries first

Scores run from 1 (worst) to 5 (best). For *compliance* and *competition*, 5 means **low** risk or crowding. US sizes come from Census NES 2023 (see the main report §3.1).

| Industry | US solo businesses (≥$50K) | Size | Digital intensity | Repeatable workflows | Willingness to pay | Compliance (5 = low risk) | Competition (5 = open) | **Total /30** | Phase |
|---|---|---|---|---|---|---|---|---|---|
| **Consultants** | 1.08M (284K) | 5 | 5 | 4 | 5 | 5 | 4 | **28** | **1** |
| **Coaches** | ICF 123K practitioners; spread across 5416/611/81299 | 3 | 5 | 4 | 4 | 4 | 3 | **23** | **1** |
| **Creators** | 1.09M (128K) | 4 | 5 | 5 | 3 | 4 | 2 | **23** | **1** |
| **Designers + marketing freelancers** | 278K + 208K (112K) | 3 | 5 | 3 | 3 | 5 | 4 | **23** | **1** |
| **Property agents** | 824K (280K); NAR 1.44M | 5 | 4 | 5 | 5 | 2 | 2 | **23** | **2** (needs compliance guardrails) |
| IT and software freelancers | 343K (96K) | 3 | 5 | 3 | 4 | 4 | 2 | 21 | 2 |
| Bookkeepers, accountants | 397K (72K) | 3 | 5 | 5 | 3 | 3 | 2 (Intuit agents) | 21 | 2 |
| Lawyers (solo) | 274K (107K) | 4 | 4 | 3 | 5 | 1 (professional rules) | 2 | 19 | 3 |
| Photographers | 237K (39K) | 2 | 3 | 3 | 2 | 5 | 3 | 18 | 3 |
| Therapists | 226K (88K) | 3 | 3 | 3 | 4 | 1 (HIPAA) | 3 | 17 | 3 |
| Tutors and instructors | 894K (69K) | 2 | 3 | 4 | 2 | 3 (minors) | 3 | 17 | 3 |

Scores are judgment calls based on the evidence above. Validate the ranking with Phase 0 interviews before committing roadmap.

**Phase 1 kits:** Consultant, Coach, Creator, and Creative freelancer (designer/marketer). Coach and Creator share a *content engine*, so four kits need about three engines of work. **Phase 2:** Property agent (largest paying segment after consultants, with a proven $299/mo price point) once its Fair Housing and TCPA guardrails are built.

## 4. Anatomy of a kit

A kit is a **company template** (it extends Paperclip's ClipHub / teams-catalog format) with six parts:

| Part | What it contains | Paperclip mapping |
|---|---|---|
| **Business profile interview** | 8–12 questions: offer, ideal client, prices, voice samples, tools, calendar, what *never* to say | Company goal + an issue document ("profile") |
| **Team cards** | 3–5 named roles shown to the user (for example Chief of Staff, Pipeline, Content, Client Desk). Internally these are **skills and workflows**, not always-on agents. | Agents / skills in the teams catalog |
| **Recurring workflows** | Trigger → steps → **outcome contract** → approval point → delivery → follow-up | Routines, issues, execution policy, monitors |
| **Guardrails** | Compliance checks, banned claims, approval defaults, connection scopes | Approvals ("Ask first"), low-trust presets, budgets |
| **First-week plan** | 5–7 quick wins seeded as tasks, so value shows up in the first session | Seed tasks |
| **Eval suite** | 20–50 golden tasks per workflow, a rubric per deliverable, pass^3 targets | Runner/Product evals, extended per kit |

Every workflow is described in this format:

```yaml
workflow: weekly_thought_leadership
trigger: schedule(mon 08:00 local)            # event or low-frequency schedule, never a tight heartbeat
inputs: [business_profile, last_4_weeks_posts, 3 industry news items (web)]
steps: [pick_topics, draft_posts, self_check, grader_review, request_approval, schedule_posts]
outcome_contract:
  deliverable: 3 LinkedIn posts + 1 newsletter draft
  must: [one idea per post, <= 220 words, ends with a question or CTA,
         matches voice profile (grader >= 4/5), no uncited statistics, no client names]
  checks: [length, banned_phrases, link_validity, duplicate_vs_history]   # deterministic
  grader: rubric_v3 (independent context, cheap model)
  max_revisions: 2
approval: required (trust ladder may auto-approve after 20 consecutive unedited approvals)
budget: $0.60 per run hard cap
kpis: [posts_published, approval_without_edit_rate, engagement_delta]
```

## 5. Phase 1 and Phase 2 kits in detail

### 5.1 Consultant kit ("Your consulting firm of one")
**Team:** Chief of Staff · Pipeline · Thought Leadership · Proposal Desk · Client Desk
**Connections:** Gmail / Google Workspace, Calendar, meeting notes (the repo already documents a Fireflies connection), Stripe or QuickBooks, LinkedIn (through a scheduler, within its terms)

| Workflow | Trigger | Definition of done (outcome contract) | Approval |
|---|---|---|---|
| Pipeline follow-ups | Daily scan of CRM sheet / inbox | No open opportunity untouched for more than *N* days. Each draft references the last conversation. | Send requires approval; eligible for trust-ladder auto |
| Discovery call → proposal | New meeting transcript | Every client-stated goal addressed (checked against the transcript); pricing matches the rate card; scope, timeline and three options present | Always |
| Weekly thought leadership | Monday | See the YAML above | Always at first |
| Client onboarding | Deal marked won | Welcome email, intake form, kickoff agenda, shared folder created; all links valid | First send |
| Invoicing and receivables | Milestone or date | Invoice total equals the contract milestone; reminders at +7 / +14 days; stops when paid | First reminder |
| Weekly company report | Friday | Pipeline value, proposals, content shipped, receivable days, **what didn't work**, cost | n/a |

**KPIs:** days from call to proposal · leads touched per week · proposal win rate · receivable days · approval-without-edit rate.

### 5.2 Coach kit ("Your coaching business, on schedule")
**Team:** Chief of Staff · Content Engine · Launch Manager · Client Care
**Connections:** Email and newsletter tool, calendar and booking, community platform, payments

| Workflow | Definition of done | Guardrails |
|---|---|---|
| Weekly content engine (posts, email, short-video scripts) | Cadence met; voice match; one call to action per piece | No health, medical or financial outcome claims (grader check) |
| Launch sequence (webinar or challenge) | Calendar of 10–14 assets, each drafted and scheduled; links tested | Earnings claims blocked; FTC testimonial rules |
| Client onboarding | Intake + scheduling + welcome kit delivered within 24 hours of purchase | — |
| Session follow-up | Notes → action items → check-in message within 24 hours | Client data kept private; AI disclosure where the EU AI Act applies |
| Testimonial collection | Ask sent after milestone; consent captured before use | FTC Endorsement Guides |

### 5.3 Creator kit ("Your media company of one")
**Team:** Producer · Repurposer · Partnerships · Community
**Connections:** YouTube / podcast host, newsletter, social schedulers, email, sponsorship tracking sheet

| Workflow | Definition of done | Guardrails |
|---|---|---|
| Repurpose long-form content (clips, threads, newsletter) | N assets per episode; timestamps verified against the transcript; no misquotes | Platform terms: use official APIs and schedulers, no bot engagement |
| Sponsorship pipeline | Media kit current; outreach to a target list; every deal tracked to an invoice | #ad / FTC disclosure inserted and verified |
| Community replies | Draft replies to top comments and DMs; flag risky ones | Never auto-reply to minors or sensitive topics |
| Weekly analytics report | Growth, top content, next-week plan | — |

### 5.4 Creative freelancer kit (designers and marketers)
**Team:** Studio Manager · New Business · Case Studies · Billing

| Workflow | Definition of done |
|---|---|
| Brief → project plan | Scope, deliverables, revision rounds and timeline confirmed with the client |
| Revision tracker | Every client comment mapped to a change or a reply; nothing dropped |
| Case study from finished project | Problem → process → result, client approval obtained, published to portfolio |
| New-business proposals | Tailored proposals to qualified leads (job-board terms respected, e.g. no automated Upwork submissions) |
| Invoicing and receivables | As in the Consultant kit |

### 5.5 Property agent kit (Phase 2; compliance first)
**Team:** Lead Desk · Listing Launch · Sphere Nurture · Transaction Coordinator

| Workflow | Definition of done | Guardrails (must be built before launch) |
|---|---|---|
| Speed to lead | First response within minutes; qualification questions asked; handoff to the agent | **TCPA** consent before texts; opt-out honored; quiet hours |
| Listing launch | Description, social posts, email to sphere, open-house plan; facts match the MLS entry | **Fair Housing** advertising language checker (no steering or protected-class references) |
| Sphere nurture | Monthly touch to past clients with a local market update (sourced numbers) | CAN-SPAM; data sources cited |
| Transaction timeline | All contract contingency dates on the calendar with reminders | Human confirms every date extracted from contracts |

**Competition:** Lofty ($299/mo "Agentic OS"), Follow Up Boss, kvCORE. **Differentiation:** a cheaper full solo kit, verified outcomes, and compliance checks built in rather than bolted on.

### 5.6 Later kits (sketch)
- **E-commerce seller.** Product copy, reviews → support, promotions. Integrate with Shopify Sidekick rather than compete with it.
- **Bookkeeper.** Month-end close checklists, client document chasing. QuickBooks agents overlap.
- **IT freelancer.** Proposals, client reporting, maintenance summaries.
- **Lawyer / therapist.** Only with professional-rules and HIPAA review. Start with the non-client-facing admin jobs.

## 6. Kit marketplace (category and community flywheel)

- **First-party kits first** (Phase 1), each with published outcome metrics: acceptance rate and cost per deliverable.
- **Then community kits.** Experienced operators (consultants, coaches) publish kits built on their own playbooks. They are paid per install or subscription. **Users never pay a share of their own revenue.**
- **Quality gate:** community kits must pass the kit's eval suite (pass^3 thresholds) before they are listed. This avoids the GPT Store's discovery and quality problem.
- This extends ClipHub's "download a company" concept from `doc/CLIPHUB.md` to non-developers.

## 7. What to validate in Phase 0

1. Interview 8 people per Phase 1 industry. List their 10 most frequent recurring jobs and mark which they would approve without editing.
2. Run a landing-page test of kit pages vs a generic page. Compare conversion and time to first accepted deliverable.
3. During the concierge pilot, measure each workflow's **first-pass acceptance** and **cost per accepted deliverable**. Drop or redesign workflows below 60% acceptance.
