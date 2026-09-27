# Product Strategy: What to Build for Non-Technical One-Person Companies

**Date:** 2026-09-27
**Author role:** Chief Product Officer
**Part of:** [Market research](./market-research.md) · [Industry kits](./industry-kits.md) · [Reliability and cost harness](./reliability-cost-harness.md) · [Marketing plan](./marketing-plan.md)
**Question:** Which features should we build so that non-technical one-person-company (OPC) owners get results 10–100x better than today, and clearly better than the competitors?

**Method:**
1. **Voice of customer.** 731 public Trustpilot reviews of nine competitors (539 negative, 192 five-star), collected on 2026-09-27 and coded by theme.
2. **Where the owner's week goes.** Studies on admin time, lead response, missed calls, late invoices and content time.
3. **UX research on non-technical AI users.** Nielsen Norman Group, approval-fatigue research, age and mobile data.
4. **Competitor capability teardown.** ChatGPT Work, Claude Cowork, Genspark Claw, Lindy, Motion, Sintra, Marblism, HoneyBook, Polsia and NanoCorp.
5. **Codebase review** of what Paperclip already provides.

Where a number is an estimate or a target rather than measured data, it says so.

---

## 0. The decision on one page

**Product thesis.** Non-technical owners don't want "AI agents." They want to **stop losing leads, get paid, show up consistently, and get their evenings back**, without risking their reputation or their wallet. Competitors compete on AI capability: more agents, more apps, more autonomy. Our customers are failing on something else: **trust** (billing, support, unwanted actions), **starting** (they don't know what to ask), **approval burden**, and **results they can't see.** We win by changing:
- the unit of value, from *AI tasks* to **verified business outcomes**;
- the interaction, from *prompting and configuring* to **deciding** ("approve, edit, skip").

**The seven bets that make us different** (details in §3):

| # | Bet | The 10–100x claim we will try to prove |
|---|---|---|
| B1 | **Zero-prompt start:** a Business X-ray plus a Business Brain | Useful results in **< 10 minutes with zero prompts** (vs hours of setup or a blank chat box) |
| B2 | **A front office that never sleeps:** answer every lead in minutes, 24/7 | First reply in **< 5 minutes vs a 42–47 hour average** (~500x faster); leads never answered: **42.6% → < 1%** |
| B3 | **The revenue loop:** follow-ups → proposals → invoices → paid | Invoice-chasing time from **> 1 workday a month to minutes**; proposals out the same day instead of days later |
| B4 | **Verified work:** outcome contracts, checks, and "failed jobs are free" | **$0 paid for failed work** (competitors burn credits on stuck tasks) |
| B5 | **Decisions, not approvals:** a risk-tiered inbox, batch approvals, and a trust ladder backed by evidence | **Approve the whole week in about 3 minutes** instead of item by item |
| B6 | **Fair economics and real humans:** a billing center, no credits, human support with a response-time promise | Removes the **#1 (billing, 53%)** and **#2 (support, 40%)** complaint categories in the market |
| B7 | **The CEO's Friday:** an honest weekly review, an opportunity radar, and community benchmarks | Owners see money recovered and hours returned every week; that is our retention engine |

**What we will not build:**
- Org charts, agent editors or prompt libraries as the main interface.
- "A company from one sentence."
- Credits or a revenue share.
- Full autonomy by default, or moving money without approval.
- AI clones that talk to clients.
- A general chat app, a workflow canvas, or a full CRM, accounting or website builder. We integrate with those instead.

Details in §9.

**Scope.**
- **MVP for the January 2027 launch** is items F1–F15 in §6, about 70 person-weeks of build on top of what Paperclip already has.
- **Cut line if the team is smaller than ~6 builders:** ship the core (~49 person-weeks) at launch and move Get-paid, X-ray, the content engine and proposals to W+4.
- **Next (Feb–Apr 2027):** the trust ladder, voice and messaging-app channels, the AI receptionist alongside the Property agent kit, the opportunity radar, and accounting sync.
- **Later:** the kit marketplace and benchmarks, a client portal, and human expert escalation.

**How we'll know it's working:** per-job metrics (§4) sit under the existing North Star (weekly accepted deliverables per active company), plus two owner-facing metrics: **hours returned per week** and **money recovered** (leads answered in time, overdue invoices collected).

---

## 1. What customers are telling us

### 1.1 Voice of customer: 731 competitor reviews

We collected Trustpilot reviews for nine products that sell AI "employees," agents or AI business building to small businesses. We coded each review by theme with keyword rules, then validated the rules by reading a random sample. One review can carry several themes.

**Review base:**

| Product | Trustpilot score | Total reviews | Negative reviews analyzed |
|---|---|---|---|
| Sintra AI | 4.4 | 8,659 | 97 |
| Motion | 3.7 | 578 | 92 |
| Polsia | 3.2 | 284 | 84 |
| Manus | 1.2 | 208 | 77 |
| Genspark | 3.8 | 444 | 62 |
| Marblism | 4.8 | 1,134 | 36 |
| Taskade | 4.6 | 781 | 35 |
| Lindy | 1.7 | 40 | 34 |
| Durable | 4.8 | 328 | 22 |

**What goes wrong** (539 one- and two-star reviews):

| Theme | Share of negative reviews | What it means for us |
|---|---|---|
| **Billing, cancellation and refunds** | **53.1%** | The most common failure isn't the AI at all. Billing has to be a *product* feature: see F1. |
| **Unresponsive support** | **39.5%** | Human help with a response-time promise is a differentiator: F2. |
| **Credits and usage limits** | **37.1%** | Customers hate meters, surprise limits, and plans changed from "unlimited" to credits: F3. |
| **Bugs, errors and reliability** | 26.5% | Outcome loop, status visibility, failed jobs free: B4. |
| **Output quality** (generic, wrong, hallucinated) | 18.7% | Business Brain plus checks and grader: B1, B4. |
| **Price / value** | 18.4% | Show value weekly (money recovered, hours returned): B7. |
| **Overpromised; doesn't actually do the work** | 13.7% | Honest capability map; Friday review: B7. |
| **Integrations and connections** | 8.7% | Keep-your-number phone; native Gmail/Calendar/Stripe. |
| **Data, privacy and lock-in** | 8.3% | Export everything; no platform-held domains: F14. |
| **Unwanted actions** | 4.8% (low count, high severity) | Risk tiers, undo, "never hide or move my email": F5, F15. |
| **Memory and personalization** | 4.5% (a top *delighter* in positive reviews) | Business Brain: B1. |
| **Complexity and learning curve** | 4.1% | Zero-prompt start. This share is low because complex products lose non-technical buyers before they write reviews. |

**Where each competitor fails most:**

| Product | Top complaint themes |
|---|---|
| Sintra | Credits 60%, billing 56% |
| Motion | Billing 75% |
| Genspark | Credits 63% |
| Manus | Billing 58%, support 55% |
| Polsia | Billing 45%, reliability 38% |
| Marblism | Reliability 36%, quality 33% |

**What customers love** (192 five-star reviews):

| Theme | Share of positive reviews |
|---|---|
| Time saved | 35% |
| Organization and planning | 26% |
| "Feels like a team or assistant" | 17% |
| Easy for non-technical users | 17% |
| A named human support person | 16% |
| Business results (leads, clients, sales) | 14% |

**Quotes that shaped this strategy** (excerpts, 2026):

| Source | Quote | Signal |
|---|---|---|
| Sintra, 2★ | "If I have to approve every little post, then that's the same as me just doing the post myself." | Approval fatigue kills the value, so we need B5 |
| Sintra, 1★ | Paid for an "unlimited" plan; after ~2 years it was "suddenly changed … to a restrictive credit-based system." | Grandfathering promise, no credits (F1, F3) |
| Genspark, 1★ | "Monthly Credits last just one day!" | Meters destroy trust |
| Manus, 1★ | Reported a "6,835 credit loss from stuck Agent task." | Failed jobs must be free (F3) |
| Lindy, 1★ | "It auto-moved all email invitations … to a hidden folder … I missed a few important meetings." | Safe-action rules; never hide or move without asking (F15) |
| Marblism, 2★ | "The only way for this to work is to change my business number … No company is going to change their primary number." | Keep-your-number receptionist (F21) |
| Marblism, 1★ | "Email marketer has put our brand at risk with absurd emails." | Checks, grader, approvals (B4, B5) |
| Polsia, 1★ | "3 months, $0 revenue … app never provisioned." | Measure outcomes honestly (B7) |
| Taskade, 1★ | Wrote to support four times at $200/mo, "No one has responded." | Human support promise (F2) |
| Sintra, 5★ | "I don't have to reexplain what I do for a living all the time!" | Business Brain is a delighter (B1) |
| Polsia, 5★ | "I'm 64 years and trying so hard to start my own business with AI." | Accessibility for older and non-technical owners |

### 1.2 Where the owner's week and money leak

| Leak | Data | Source |
|---|---|---|
| Admin load | Surveys: 11–16 hours/week, about 36% of the work week. Time-tracking data shows owners **underestimate admin by 35–50%**. | [Stealth Agents compilation](https://stealthagents.com/research/startup-admin-burden-statistics-2026), [Agility PR](https://www.agilitypr.com/pr-news/pr-news-trends/time-management-new-survey-reveals-biz-owners-spending-time-theyd-rather-spend/) |
| Slow or no lead response | Average first response **42–47 hours**. Only **3.1%** of web-form leads get a reply within 5 minutes; **42.6% are never answered**. | [Prospeo](https://prospeo.io/s/average-lead-response-time), [AInora study roundup](https://ainora.lt/blog/lead-response-time-statistics-every-study-2026), [Leadferno](https://leadferno.com/blog/research-website-contact-forms-and-lead-management-uncovering-costly-mistakes) |
| Why speed matters | Leads contacted within 5 minutes are **21x more likely to qualify** than at 30 minutes (MIT/InsideSales; vendor data, not a controlled trial) | [Vesma research note](https://vesma.app/resources/lead-response-time-research) |
| Missed calls | Small businesses answer **37.8%** of inbound calls; **85%** of missed callers never call back (secondary compilations) | [AInora missed-call stats](https://ainora.lt/blog/missed-call-statistics-small-business-2026), [Aira](https://www.getaira.io/blog/missed-business-calls-statistics) |
| Late payment | Average wait **28.8 days** (Xero small-business data, via compilation). **56%** of small businesses have unpaid invoices, averaging **$17.5K**. Freelancers spend **more than a full workday a month** chasing payment. | [QuickBooks late payments report](https://quickbooks.intuit.com/r/small-business-data/small-business-late-payments-report-2025/), [Clockify](https://clockify.me/late-invoice-statistics) |
| Content | About **6 hours/week** on social media, mostly creating content | [Picmim roundup](https://blog.picmim.com/blog/how-much-time-companies-spend-social-media) |
| Tool sprawl | About 2 hours/week spent moving data between apps (secondary) | [Breeze](https://www.breeze.pm/articles/saas-tool-sprawl-statistics) |
| What owners would hand to AI "if they could trust it to do it perfectly" | Bookkeeping and taxes (17%), creative marketing (15%) | [QuickBooks 2026 Business Owner Report](https://quickbooks.intuit.com/r/small-business-data/business-ownership-in-2026/) |
| What AI-using small businesses use it for | Marketing content (68%), customer communication (52%), admin (47%) (NFIB 2026, via compilation) | [Booth Associates](https://boothassociatesllc.com/ai-statistics-small-business-2026.html) |

**Takeaway:** the biggest 10x opportunities are where *speed and consistency* decide the money (lead response, follow-up, collections), not where AI writes nicer text.

### 1.3 Why non-technical users stall

- **The articulation barrier.** Getting value from a chat box takes three steps: know what the AI can do, decide what you want, then describe it in writing. Jakob Nielsen estimates that "half the population can't do it" well ([NN/g](https://www.nngroup.com/articles/ai-articulation-barrier/)). **Design implication:** the product *proposes*; the owner *chooses*. Voice is easier than writing.
- **Trust is falling while adoption rises.** NN/g's State of UX 2026 calls trust the defining AI design problem; transparency, control, consistency and support when things fail are the fundamentals ([NN/g](https://www.nngroup.com/articles/state-of-ux-2026/)).
- **Approval fatigue and automation bias.** Frequent approvals decay into rubber stamps, and people over-trust confident AI output ([TianPan](https://tianpan.co/blog/2026/06/25/approval-fatigue-how-human-in-the-loop-gates-decay-into-rubber-stamps), [TechTarget](https://www.techtarget.com/it-strategy/feature/Human-in-the-loop-shouldnt-rubber-stamp-decisions)). **Design implication:** fewer, better decisions, tiered by risk, with evidence shown.
- **Age.** Self-employment rises with age: 25% of workers aged 55–59 and 46% aged 65–69 are self-employed ([AARP / NBER](https://www.aarp.org/pri/topics/work-finances-retirement/employers-workforce/older-workers-self-employment/)). **Design implication:** large type, plain language, voice, patient human help.
- **Phones and messaging apps.** 80% of small-business owners in India and Brazil run their business on WhatsApp, and business messages are opened ~98% of the time versus ~20% for email (secondary) ([Infobip](https://www.infobip.com/blog/whatsapp-statistics), [YCloud](https://www.ycloud.com/blog/whatsapp-statistics-for-businesses)). Owners also work after 10 p.m. about 9 times a month ([Founder Reports](https://founderreports.com/solopreneur-statistics/)). **Design implication:** approvals and briefs where the owner already is, with quiet hours.

### 1.4 What competitors already do (the late-2026 baseline)

| Capability | ChatGPT Work | Claude Cowork | Genspark Claw | Lindy | Motion | Sintra | Marblism | HoneyBook | Polsia / NanoCorp |
|---|---|---|---|---|---|---|---|---|---|
| Scheduled or recurring work | ✅ | ✅ | ✅ | ✅ | ✅ | ◐ | ✅ | ✅ (rules) | ✅ |
| Connectors (email, calendar, docs) | ✅ plugins | ✅ plugins | ✅ 631+ apps | ✅ thousands + MCP | ◐ | ✅ (claims 1,000+) | ◐ | ✅ | ◐ |
| Plan-before-act and action approvals | ✅ plan mode, check-ins, approvals | ◐ | ◐ | ✅ approvals built in | ◐ | ◐ (approve posts) | ◐ | n/a | ❌ ("no human in the loop") |
| Persistent business memory | ◐ projects and memory | ◐ folder instructions | ✅ | ✅ workspace context | ◐ | ✅ "Brain AI" | ◐ (users report "little memory") | ◐ client records | ◐ |
| Phone and messaging-app access | ◐ mobile | ✅ Dispatch from phone | ✅ WhatsApp, Telegram, calls | ✅ iMessage | ◐ | ◐ | ✅ receptionist (number change required) | ◐ | ◐ |
| Front office (answer leads, calls, inquiries) | ❌ | ❌ | ◐ outbound calls | ◐ inbox | ◐ AI SDR books calls | ◐ support helper | ✅ receptionist | ◐ inquiry auto-reply | ◐ customer replies |
| Money loop (invoice, chase, collect) | ◐ via Intuit plugin | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ invoices, payments, reminders | ◐ checkout |
| Verified completion (definition of done, independent checks) | ◐ | ◐ | ❌ | ❌ | ❌ | ❌ | ❌ | n/a | ❌ |
| Industry playbooks | ◐ small-business skills | ◐ role plugins | ❌ | ◐ | ◐ industry pages | ◐ role helpers | ❌ | ✅ creative-industry templates | ❌ |
| Honest weekly results | ❌ | ❌ | ❌ | ◐ daily briefs | ◐ | ❌ | ❌ | ◐ reports | ◐ NanoCorp leaderboard |
| Pricing model | Bundled into ChatGPT plans | Claude plans | Credits | Credits per seat | Seats + credits | Credits | Flat $24 ("50h of work") | Flat $29–$129 | Subscription + 20% of revenue |

Legend: ✅ strong · ◐ partial · ❌ absent. This is a judgment from public product pages, docs and reviews dated 2026-09.

Sources: [ChatGPT Work](https://thenextweb.com/news/openai-chatgpt-work-agent-launch) · [Claude Cowork scheduled tasks](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork) and [Dispatch](https://support.claude.com/en/articles/13947068-assign-tasks-from-anywhere-in-claude-cowork) · [Genspark Claw](https://www.genspark.ai/genspark-claw) · [Lindy pricing and features](https://www.lindy.ai/pricing) · [Motion AI employees](https://www.usemotion.com/ai-employees/ai-sdr) · [Sintra](https://sintra.ai/pricing) · [Marblism](https://www.marblism.com/pricing) · [HoneyBook](https://www.softwareadvice.com/crm/honeybook-profile/) and [comparison](https://www.solopad.io/blog/honeybook-vs-dubsado-vs-bonsai).

**Implication:**
- **Table stakes (we must have them; they don't differentiate):** scheduled tasks, connectors, action approvals, plan-before-act, memory, mobile access, drafting in your voice.
- **Unclaimed ground (where we win):**
  - verified outcomes and fair economics;
  - a front office *combined with* a money loop on one Business Brain;
  - decision design that doesn't wear the owner out;
  - honest weekly results;
  - industry kits with published benchmarks.
- **Direct incumbent:** HoneyBook owns "client flow" for creative solo businesses at $29–$129/mo, but it runs rules, not agents. No one in the HoneyBook/Dubsado/Bonsai group has AI that does the heavy lifting ([SoloPad](https://www.solopad.io/blog/honeybook-vs-dubsado-vs-bonsai)). **We should do the work that their rules can't, and integrate with HoneyBook rather than replace it.**

---

## 2. Product principles for non-technical owners

1. **Zero prompts to value.** Every kit job starts from the product's own proposal. Typing is optional; voice is welcome.
2. **Show, don't ask.** Offer 2–3 concrete options ("Send A / Send B / Skip") instead of open questions (NN/g's hybrid-interface guidance).
3. **Decisions, not configuration.** The owner sets *policies* ("always OK to confirm meeting times") in plain sentences. There are no rule builders.
4. **Risk decides the interruption.** Internal and reversible actions just happen. Outward-facing, reversible ones are batched with an undo window. Money, contracts, new commitments and public statements always get an explicit OK.
5. **Every action is explainable and undoable.** "What I did and why," in one sentence, next to an undo button where the world allows it.
6. **Respect the owner's time.** Batch decisions into one or two windows a day; honor quiet hours; one Friday review.
7. **Honest by default.** Report what failed. Never charge for failed work. Never claim outcomes we can't show.
8. **Meet them where they are.** Phone first; email, iMessage and WhatsApp for briefs and approvals; voice notes for instructions.
9. **Progressive autonomy, earned with evidence.** Autonomy grows per action type, based on the owner's own approval history.
10. **Accessible to everyone.** Grade 6–8 reading level; WCAG 2.2 AA; large-type and voice modes; localization for expansion markets.

---

## 3. The seven bets in detail

### B1. Zero-prompt start: Business X-ray + Business Brain

**Problem.** The articulation barrier, and "I don't have to re-explain what I do" is a top delighter. Output-quality complaints (19%) mostly come from a lack of context.

**What we build:**
- **Business X-ray (onboarding magic moment):**
  1. The owner connects Gmail/Outlook, Calendar and, optionally, Stripe or QuickBooks, **read-only first**.
  2. In about 2 minutes the product shows **"money on the table"**: unanswered leads (and how old they are), stalled proposals, overdue invoices and amounts, past clients with no contact in 90+ days, and upcoming meetings with no prep.
  3. Each finding comes with a pre-drafted action ready to approve.
- **Business Brain:**
  - A structured, owner-editable profile: offers and prices, ideal clients, active clients and deals, tone of voice (learned from sent mail), availability, and policies ("never discount more than 10%").
  - It is shown as **"What I know about your business,"** with "correct this" on every line.
  - It learns from every edit the owner makes.
- **Five-minute interview** (voice or text) for anything the data doesn't reveal.

**Why 10–100x:**
- **Time to first useful result:** under 10 minutes with zero prompts. Self-hosting Paperclip is "8+ hours" by a hosting vendor's own estimate ([PaperclipCloud](https://paperclipcloud.com/)), and a chat assistant starts from a blank box.
- **Better output from the start:** results begin grounded in the owner's own data and voice instead of generic text.

**Competitor status.** Sintra's "Brain AI" and Genspark's persistent memory hold context, but no competitor turns the owner's *own data* into a quantified "money on the table" view at first run.

**Paperclip reuse:** the company goal plus issue documents for the profile; company skills; experimental memory connectors (`doc/connections/MEMORY.md`); Gmail and Google Workspace connections.

**Guardrails:**
- Read-only by default; explicit scopes explained in plain words.
- Nothing is sent during the X-ray.
- A data-use promise that we don't train on customer data.
- Findings stay local to the company.

**MVP:** X-ray *lite* covers unanswered leads, overdue invoices and stale proposals, plus Brain v1.

### B2. A front office that never sleeps

**Problem.** Average lead response is 42–47 hours, 42.6% of web leads are never answered, and 62% of calls go unanswered. Marblism customers refuse to change their phone number.

**What we build:**
- **Speed-to-lead (MVP):**
  - Watch the inbox and web-form notifications.
  - Classify leads.
  - Reply within minutes, around the clock, using the Brain: answer the question, offer booking times, and qualify.
  - Every first reply to a *new* contact goes through a policy the owner sets once ("reply to inquiries about X automatically; ask me about Y").
- **An assistant email identity:** `assistant@yourdomain`, via the existing AgentMail connection. This keeps a clear line between the owner and the AI (Next).
- **AI receptionist that keeps your number** (Next, launching with the Property agent kit):
  - Conditional forwarding on busy or no-answer: the owner's calls ring as normal, and only missed calls roll to the AI. Every carrier supports this ([SkipCalls guide](https://skipcalls.com/solutions/call-forwarding-setup)).
  - It books straight onto the calendar, creates the lead, triggers follow-up, and texts the owner a summary.
  - Telephony comes from a voice partner. Market cost is about $0.09–0.36 per minute all-in ([Famulor](https://www.famulor.io/blog/ai-voice-agent-pricing-2026-what-10-platforms-actually-cost-per-minute)).

**Why 10–100x:**
- **First response** in under 5 minutes versus 42–47 hours: roughly 500x faster.
- **Qualification odds** rise up to 21x (MIT/InsideSales).
- **Never-answered leads** fall from 42.6% to under 1%: about 40x fewer.
- **Calls:** answered or captured goes from ~38% to ~100%. That is 2.6x more coverage, and it matters more than the multiple suggests, because 85% of missed callers never call back.

**Competitor status.** Marblism has a receptionist but requires a number change. Motion's AI SDR books calls for sales teams. Nobody combines the front office with the same Brain that runs follow-ups, proposals and invoicing.

**Paperclip reuse:** routines with webhook and API triggers; AgentMail inbox-to-task mapping; low-trust review for inbound content (prompt-injection defense, `doc/LOW-TRUST-PRESETS.md`).

**Guardrails:**
- The AI discloses that it is AI where the EU AI Act Article 50 applies, and by default everywhere.
- Call-recording consent follows the rules of each US state.
- TCPA consent is required before any text message.
- Quiet hours.
- Human handoff on request.

### B3. The revenue loop: follow-ups → proposals → invoices → paid

**Problem.** Deals die from missed follow-ups. Proposals take days. 56% of small businesses carry overdue invoices, averaging $17.5K. Chasing payment eats more than a workday a month.

**What we build:**
- **Follow-up engine:** every open conversation gets a next step. Nothing stays untouched longer than N days (from the Consultant kit).
- **Proposal from call:** meeting transcript or voice note → a proposal checked against the client's stated goals and the owner's rate card. Ready to approve within the hour.
- **Get-paid autopilot:**
  - Stripe-hosted invoices and payment links; we never hold funds.
  - Polite reminders at +3, +7 and +14 days, in the owner's voice.
  - Escalation suggestions, and a cash-flow view showing what comes in and when.
- **Accounting sync (Next):** QuickBooks/Xero, with receipts and categorization prepared for the owner's bookkeeper. Bookkeeping and taxes is the #1 job owners would hand to AI "if they could trust it."

**Why 10–100x:**
- Invoice chasing drops from more than a workday a month to under 15 minutes of approvals: roughly 30x.
- Proposal turnaround goes from days to under an hour: 10–50x. This needs pilot measurement.
- No follow-up is ever forgotten, so coverage approaches 100%.

**Competitor status.** HoneyBook automates rule-based client flow and invoicing but doesn't do the work agentically. AI-employee bundles don't touch money.

**Paperclip reuse:** monitors (`executionPolicy.monitor`) for "did they pay or reply?"; tool-action approvals with signed arguments for anything that touches money.

**Guardrails:**
- Stripe and QuickBooks writes are deliberately *not* in Paperclip's first connector batch because of finance risk (`doc/connections/FIRST-30-MATRIX.md`). So we start with drafts that need approval, and Stripe-hosted invoices.
- No autonomous money movement.
- Refunds, discounts and write-offs always need an explicit OK.

### B4. Verified work: outcome contracts and "failed jobs are free"

**Problem.** Reliability complaints (27%), credits burned on stuck tasks, and brand-damaging output.

**What we build:**
- Every job carries an **outcome contract**: a visible definition of done, deterministic checks, an independent grader, and a budget cap. The full design is in the [harness document](./reliability-cost-harness.md).
- If a job can't meet its contract, the owner gets **"couldn't finish, here's why"** with the partial work, and **it doesn't count against the plan**.
- Automatic credit for any job that failed after the owner had approved it.
- A per-kit **reliability page** showing published first-pass acceptance and on-time rates.

**Why 10–100x:** the cost of failed work to the owner drops to **$0**, versus paying for failures under credit systems. First-pass acceptance targets are ≥60% at launch and ≥80% by month 3.

**Competitor status.** None publish completion guarantees. Intercom Fin's "$0.99 per resolution" shows that outcome-linked pricing is accepted in adjacent markets ([Fin pricing](https://fin.ai/pricing)).

**Paperclip reuse, the strongest part of this bet:**
- **`completion_contracts` already exists**, with risk level, completion authority, an incomplete-criteria policy and contract JSON.
- `work_assessments` and `status_decisions` already hold the evidence chain.
- Native completion reviews, the task watchdog, and recovery with three attempts are in place.

We expose these as plain-language "done means…" cards.

### B5. Decisions, not approvals

**Problem.** A Sintra reviewer: "If I have to approve every little post … same as me just doing the post myself." Research on approval fatigue shows that too many approvals turn into rubber stamps. On the other side, unwanted actions (Lindy hiding meeting invites) destroy trust.

**What we build:**
- **A risk-tiered decision inbox:**

  | Risk | Examples | Handling |
  |---|---|---|
  | **Low** | Internal, reversible actions | Just happens; logged |
  | **Medium** | Outward-facing but reversible | Batched: "approve these 12 posts," with a 60-second undo-send window |
  | **High** | Money, contracts, new commitments, public claims | Individual approval with a one-line risk explanation |

- **"Approve the week":** a Monday plan the owner approves once. Individual items only interrupt if they change materially.
- **Swipe triage on mobile:** approve / edit / skip in under 5 seconds each, with the evidence visible.
- **Policies in plain sentences:** "Always OK to confirm meeting times." "Never mention prices in first replies."
- **A trust ladder with evidence (Next):** "You've sent 47 of my follow-up drafts unchanged. Let me send these automatically, with a daily digest?" It suggests promotion but never auto-promotes money or other irreversible actions.
- **Safe-action rules:** never delete, hide or move the owner's email, files or events without asking; a plain-language activity log.
- **Quiet hours, focus windows and vacation autopilot (Next):** decisions arrive in chosen windows. While the owner is away, the product handles inbound messages and defers commitments.

**Why 10–100x:** the owner approves a week of work in about 3 minutes instead of dozens of interruptions. Approvals get *fewer and better* over time instead of fading into rubber stamps.

**Competitor status.** ChatGPT Work and Lindy have approvals, but per-action approvals are exactly what users complain about. No one ties autonomy to evidence from the owner's own history.

**Paperclip reuse:**
- The Decisions desk: decision queues with seed rules, decide-by and snooze triage, and signed bulk proposals (`doc/DATABASE.md`).
- `tool_action_requests` with "Approve & run" and remembered permissions.
- **`decision_training_examples`**, which captures owner decisions: the evidence base for the trust ladder.

### B6. Fair economics and real humans

**Problem.** Billing is 53% of complaints, support 40% and credits 37%. This is the cheapest 10x in the market: most of it is policy and service, not AI research.

**What we build:**
- **Billing center:**
  - One-click cancel or pause.
  - Prorated refunds.
  - An email 3 days before any renewal or trial charge.
  - Spend caps.
  - Invoices in one place.
  - A **grandfathering promise:** we never move a paying customer to a worse plan.
- **No credits:** a plain allowance in *jobs* and dollars that rolls over monthly. Failed jobs are free (B4).
- **Human support promise:** paid plans get a human reply within 1 business hour, plus a "talk to a human" button in the product. AI support triage escalates to a person after two unhelpful turns.
- **Status and incidents:** a public status page, proactive notice when a job type is affected, and automatic credit for the impact.
- **Data rights:** export everything (business profile, clients, documents, history) in open formats. Domains and sites are never held by the platform.

**Why 10–100x:** it turns the two most common reasons people leave reviews into reasons they recommend us. Human first response goes from "no reply" to under an hour.

**Paperclip reuse:** company import/export for portability; budget policies and incidents for caps. **New build:** the customer billing center, a support console, and the status page.

### B7. The CEO's Friday

**Problem.** "Overpromised" complaints (14%) and weak perceived value (18%). The top delighter is time saved, which owners can only feel if they can *see* it.

**What we build:**
- **Friday CEO Review:**
  - Hours returned: measured from jobs done, with the assumptions shown.
  - Money recovered: invoices collected, leads answered within 5 minutes.
  - What shipped.
  - **What didn't work, and why.**
  - What it cost.
  - Next week's plan, with one-tap "approve the week."
- **Opportunity radar (Next):** "3 past clients haven't heard from you in 90 days." "Your proposal win rate dropped this month." "Consultants in your kit raised rates 8% this year" (opt-in, anonymized benchmarks).
- **Community benchmarks and kit marketplace (Later):** experts publish kits, and aggregated anonymized results create a network effect: "what works for one-person consultancies."

**Why 10–100x:** proof of value arrives every week, which competitors don't give. It is also the share object for marketing (see [marketing plan](./marketing-plan.md) §13.3).

**Paperclip reuse:** Dashboard, Timeline, artifacts and work products, Costs.

### Supporting capabilities (must match competitors, not differentiators)

| Capability | Plan |
|---|---|
| **Content engine** | One input (voice note, call, blog post) → posts, newsletter and short-video scripts. Calendar with batch approval, published through official APIs and schedulers. Core of the Coach and Creator kits. |
| **Mobile web app** | Today, Needs-you and Friday on the phone. Approve by email at launch; iMessage (existing experimental Photon channel) and WhatsApp next. |
| **Voice-note instructions** | "After a client call, send me a voice note": transcript → follow-up plus proposal plus tasks. |
| **Integrations** | Gmail/Outlook, Calendar, Stripe, QuickBooks/Xero, Calendly/Cal.com, social schedulers, and HoneyBook (sync, don't replace). |
| **Accessibility and language** | Large type, voice mode, plain language; Korean and English/Hindi kits for the expansion markets. |

---

## 4. The 10–100x scorecard (targets to prove, not claims to publish)

| Outcome | Today (baseline) | Target | Multiple | Evidence |
|---|---|---|---|---|
| First reply to a new lead | 42–47 hours on average; 3.1% of web leads answered within 5 min | < 5 min, 24/7, for ≥95% of leads | **~500x faster** | Drift, Prospeo; MIT/InsideSales (21x qualification) |
| Leads never answered | 42.6% | < 1% | **~40x fewer** | Contact-form research |
| Calls answered or captured (Phase 2) | 37.8% | ~100% | 2.6x coverage (85% of missed callers never return) | Compilations of CallRail and others |
| Time to first useful result | Hours of setup, or a blank chat box | < 10 min, zero prompts | **~50x** | PaperclipCloud estimate; NN/g |
| Invoice-chasing time | More than 1 workday a month | < 15 min a month of approvals | **~30x** | Clockify/Bonsai |
| Proposal turnaround after a call | Days (to be measured in the pilot) | < 1 hour | **10–50x** | Pilot measurement |
| Weekly social content time | ~6 hours | ~30 min of approvals | **~12x** | LocaliQ/SBE compilations |
| Admin and operations hours overall | 11–16 hours/week | 4–6 hours/week | **~3x** (honest: not 10x overall) | Time Etc, time-tracking studies |
| Cost of equivalent human help | Part-time VA ~$1,200/mo; receptionist ~$3,100/mo | $79/mo | **15–40x cheaper** | Wage benchmarks |
| Human support first response | Often none (40% of competitor complaints) | < 1 business hour | **10x+** | Voice-of-customer analysis |
| Paying for failed work | Common under credit models | $0 | — | Voice-of-customer analysis |

**Rule:** we publish a multiple in marketing only after pilot data proves it for that job (FTC substantiation; see [marketing plan](./marketing-plan.md) §2.3). The overall admin reduction is about 3x. The 10–100x gains come from specific, high-value jobs, and we say so.

---

## 5. What the owner sees

**Five tabs:**
- **Today:** brief plus the Needs-you inbox.
- **Clients:** leads, clients and conversations, built automatically from email and calendar.
- **Work:** kit jobs, the content calendar, results.
- **Money:** invoices, payments, cash view.
- **Friday:** weekly review and goals.

**Settings:** Business Brain · Trust & approvals · Plan & billing · Connections · Help (human) · *Advanced*. Developer concepts (agents, org chart, routines, skills, runs) stay in *Advanced*, consistent with Paperclip's "three-door" rule for connections (`doc/connections/README.md`).

**Three flows that must be perfect:**
1. **The first 10 minutes:**
   1. Sign up.
   2. "What do you do?" (voice or text) plus the website URL.
   3. Connect email and calendar, read-only.
   4. **X-ray:** "7 leads waiting (3 for more than 5 days) · $4,200 overdue · 2 proposals with no reply."
   5. "Here's what I learned about your business. Correct anything."
   6. The kit is pre-selected.
   7. Three ready actions: reply to 2 leads, remind 1 invoice.
   8. Approve in one tap.
   9. A preview of Friday's review.
2. **The daily three minutes:** a morning brief (push, email or messaging app) → "4 things need you: 2 batch, 1 medium, 1 high" → swipe → done. Everything else is handled and logged.
3. **The Friday five minutes:** review → "what didn't work" → approve next week's plan.

---

## 6. Prioritized backlog (RICE)

**Scoring:**
- **Reach:** share of target owners affected (0–10).
- **Impact:** 0.5 low · 1 medium · 2 high · 3 massive.
- **Confidence:** how strong the evidence is.
- **Effort:** estimated person-weeks with Paperclip reuse.
- **Score** = Reach × Impact × Confidence ÷ Effort.

All scores are estimates to revisit after pilot data.

| Rank | ID | Feature | Bet | Reach | Impact | Confidence | Effort (pw) | Score | Phase |
|---|---|---|---|---|---|---|---|---|---|
| 1 | F1 | Fair billing center (one-click cancel/pause, prorated refunds, charge reminders, grandfathering) | B6 | 10 | 2 | 90% | 3 | **6.0** | Now |
| 2 | F4 | Friday CEO Review v1 | B7 | 10 | 2 | 90% | 3 | **6.0** | Now |
| 3 | F2 | Human support promise + status and incident notices | B6 | 10 | 2 | 80% | 3 | **5.3** | Now |
| 4 | F3 | Failed jobs never count + plain jobs meter (no credits) | B4/B6 | 10 | 2 | 80% | 3 | **5.3** | Now |
| 5 | F5 | Decision inbox: risk tiers, batch approve, undo window | B5 | 10 | 3 | 80% | 5 | **4.8** | Now |
| 6 | F14 | Export everything (portability) | B6 | 10 | 1 | 90% | 2 | **4.5** | Now |
| 7 | F6 | Speed-to-lead for email and web forms + follow-up sequences | B2/B3 | 9 | 3 | 80% | 6 | **3.6** | Now |
| 8 | F7 | Business Brain v1 (profile, offers, prices, clients, voice, rules) | B1 | 10 | 3 | 80% | 8 | **3.0** | Now |
| 9 | F8 | Outcome contracts + checks + grader on every MVP job | B4 | 10 | 3 | 80% | 8 | **3.0** | Now |
| 10 | F13 | Mobile web app (PWA) + approve-by-email | Parity | 9 | 2 | 80% | 5 | **2.9** | Now |
| 11 | F16 | Trust ladder with evidence (suggested promotions) | B5 | 8 | 2 | 70% | 4 | **2.8** | Next |
| 12 | F9 | Get-paid autopilot (Stripe-hosted invoices, reminders, overdue escalation) | B3 | 8 | 3 | 70% | 6 | **2.8** | Now |
| 13 | F10 | Business X-ray lite in onboarding | B1 | 9 | 3 | 60% | 6 | **2.7** | Now |
| 14 | F15 | Plain-language activity log + safe-action rules | B5 | 9 | 1 | 90% | 3 | **2.7** | Now |
| 15 | F17 | Voice-note instructions | Parity | 7 | 2 | 70% | 4 | **2.4** | Next |
| 16 | F19 | Assistant email identity (assistant@yourdomain) | B2 | 6 | 1 | 80% | 2 | **2.4** | Next |
| 17 | F11 | Content engine (one input to multichannel posts, calendar) | Parity | 7 | 2 | 80% | 5 | **2.2** | Now |
| 18 | F12 | Proposal from call notes or transcript | B3 | 6 | 2 | 70% | 4 | **2.1** | Now |
| 19 | F18 | WhatsApp / iMessage / SMS briefs and approvals | Parity | 7 | 2 | 70% | 5 | **2.0** | Next |
| 20 | F20 | Opportunity radar | B7 | 8 | 2 | 60% | 5 | **1.9** | Next |
| 21 | F22 | Quiet hours, focus windows, vacation autopilot | B5 | 8 | 1 | 70% | 3 | **1.9** | Next |
| 22 | F21 | AI receptionist that keeps your number | B2 | 5 | 3 | 70% | 8 | **1.3** | Next |
| 23 | F23 | Accounting sync (QuickBooks/Xero) + bookkeeping prep | B3 | 6 | 2 | 60% | 6 | **1.2** | Next |
| 24 | F25 | Client portal (accept, e-sign, pay, book) | B3 | 6 | 2 | 60% | 8 | **0.9** | Later |
| 25 | F24 | Community benchmarks + kit marketplace | B7 | 6 | 2 | 50% | 10 | **0.6** | Later |
| 26 | F26 | Human expert escalation for high-stakes jobs | B4 | 4 | 2 | 50% | 8 | **0.5** | Later |

**Reading the ranking:**
- **Cheap trust features score highest.** Billing, support, failed-jobs-free and the Friday review are small builds that remove the market's biggest complaints. Build them first; they are also marketing proof.
- **Big bets rank lower on RICE because of effort, not value.** Brain, outcome contracts, speed-to-lead and X-ray are the actual differentiation, so they stay in the MVP.
- **Scope:** the "Now" total is ~70 person-weeks. The **core cut** (F1–F8, F13, F14, F15, ~49 pw) ships at launch even with a smaller team. F9–F12 (~21 pw) can move to W+4.

---

## 7. Roadmap (aligned with the launch plan)

| Window | Build | Kit coverage | Exit criteria |
|---|---|---|---|
| **Now: MVP** (Nov 2026 → beta Jan 2027 → launch week of 25 Jan) | F1–F15 (or the core cut) | Consultant, Coach, Creator, Creative freelancer (the Creative kit can follow at W+4 if the team is small) | First accepted deliverable in < 10 min for ≥50% of trials; first-pass acceptance ≥60%; zero unresolved billing tickets > 48 h |
| **Next** (Feb–Apr 2027) | F16–F23: trust ladder, voice notes, messaging apps, assistant email, radar, quiet hours, **receptionist + Property agent kit** (spring housing season), accounting sync | + Property agent | Week-4 retention ≥ 40%; median lead response < 5 min for connected users; overdue invoices reduced vs baseline |
| **Later** (May 2027+) | F24–F26: benchmarks and marketplace, client portal, expert escalation; WhatsApp-first international kits | + Bookkeeper, IT freelancer, e-commerce (via Shopify) | Marketplace kits pass eval gates (pass^3); benchmarks opt-in ≥ 30% |

**Build vs integrate:**

| Area | Decision |
|---|---|
| CRM | *Build* a light "Clients" view from email and calendar; *sync* with HubSpot and HoneyBook. Don't build a full CRM. |
| Payments and invoicing | *Integrate* Stripe-hosted invoices and payment links. Never hold funds. QuickBooks/Xero sync comes Next. |
| Phone | *Partner* for telephony and voice (Retell/Vapi-class) plus carrier conditional forwarding. Don't build a telephony stack. |
| Scheduling | *Integrate* calendars and Calendly/Cal.com. |
| Social | *Integrate* official APIs and schedulers. |
| Websites | *Integrate* the owner's existing site and forms. No site builder (Durable, Wix and Squarespace exist). |

---

## 8. Build on Paperclip: reuse map

| Need | Paperclip today | Extend with |
|---|---|---|
| Business Brain | Company goal, issue documents, company skills, experimental memory connectors (Mem0, Zep, Supermemory, Cognee, Honcho) | A structured profile, a client and deal index, an editable "What I know" UI |
| Outcome contracts | `completion_contracts`, `work_assessments`, `status_decisions`; native completion reviews | Kit contract library; plain-language "Done means…" cards; failed-job credit hook |
| Decision inbox | Decisions desk (`WhatNeedsMe`), decision queues with seed rules, decide-by and snooze, signed bulk proposals | Risk tiers, batch approve, swipe UI, "approve the week" |
| Learning from approvals | `decision_training_examples` | Trust-ladder evidence and promotion suggestions |
| Action approvals | `tool_action_requests` (Approve & run, signed arguments, remembered permission) | Plain-sentence policies |
| Channels | AgentMail (agent email addresses), experimental iMessage Photon channel, Slack, Agent Chat | WhatsApp, SMS, a voice partner |
| Triggers | Routines with scheduled, API and webhook triggers | Gmail, form and payment events as triggers; retire tight heartbeats for kits |
| Budgets | `budget_policies`, `budget_incidents` | Jobs allowance, per-job caps, failed-job credits |
| Reliability | Task watchdog, recovery (3 attempts), monitors | Effort escalation; status-page feed |
| Outputs and reports | Artifacts and work products, Dashboard, Timeline, Costs | Results gallery and Friday review |
| Portability | Company import and export | "Export my business" (open formats) |
| Kits | Teams catalog, ClipHub concept | Kit format with contracts, guardrails and evals |

**Net-new builds:**
- Customer billing center and support console.
- Status page.
- Voice partner integration.
- WhatsApp channel.
- Stripe invoicing connector (approval-gated).
- Mobile PWA shell.
- X-ray analytics.

---

## 9. What we will not build, and why

| Anti-feature | Why not |
|---|---|
| Org charts, agent editors and prompt libraries as the main UI | The articulation barrier; the audience isn't technical. Keep them in Advanced. |
| "Launch a company from one sentence" autopilot | NanoCorp: 206 of 30,272 companies ever earned; the category sits close to FTC "AI business opportunity" enforcement |
| Credits or revenue share | Credits are the #3 complaint (37%); revenue share is the launchers' model and a trust problem |
| Full autonomy by default; moving money without approval | Unwanted-action incidents; finance risk (Paperclip defers Stripe and QuickBooks writes) |
| AI clones or avatars speaking to the owner's clients | Disclosure rules (EU Article 50, NY synthetic performers); reputation risk; out of scope |
| A general chat assistant | ChatGPT and Claude own this; bundled at no extra cost |
| A workflow canvas | n8n and Zapier exist; it contradicts "decisions, not configuration" |
| A full CRM, accounting package or website builder | HoneyBook, QuickBooks and Wix exist; integrate and do the work *across* them |
| High-volume cold outbound | Deliverability, CAN-SPAM/TCPA and brand risk; it conflicts with the honesty positioning |

---

## 10. Validation plan (concierge pilot → beta)

| Bet | Experiment | Success | Kill or rethink if |
|---|---|---|---|
| B1 X-ray and Brain | Run X-ray lite on 15 pilot users' real data | ≥70% approve a suggested action in the first session; ≥60% say "it showed me something I didn't know" | < 40% approve; privacy objections stop connections |
| B2 Speed-to-lead | Measure first-response time and reply rate for 4 weeks before and after | Median < 5 min; reply rate up vs baseline | Owners disable it over tone or quality |
| B3 Get paid | Track overdue invoices and days-to-paid before and after; self-reported chasing time | Overdue share down; chasing time < 15 min/month | Clients complain about the reminders |
| B4 Verified work | First-pass acceptance and pass^3 on golden tasks per workflow | ≥60% → ≥80% by month 3; zero false "done" | < 50% after two iterations on a workflow |
| B5 Decisions | Seconds per decision, decisions per week, batch share, approved-unchanged trend | ≤5 s median; the week approved in ≤3 min | Rubber-stamping signs: unchanged approvals combined with rising complaints |
| B6 Fair economics | Support first-response time, billing tickets, refunds, CSAT | < 1 business hour; zero billing tickets unresolved > 48 h | Support cost per customer beyond plan margin |
| B7 Friday | Open rate, "approve the week" rate, correlation with retention | ≥60% open; retention lift for engaged owners | Low opens after 4 weeks → change the format or channel |

---

## 11. Risks

| Risk | Mitigation |
|---|---|
| Scope creep: this is a lot of product | RICE order, the core cut line, integrate before building, and kits limit scope |
| Owners hesitate to connect email and money accounts | Read-only first, plain-language scopes, a visible data promise, and X-ray value shown before any write access |
| Platform catch-up (ChatGPT Work adds similar features) | Differentiate on the integrated front office + money loop + verified outcomes + fair economics + industry kits + community, not on any single feature |
| Voice and phone compliance (call recording, TCPA) | Phase 2 with a compliance review; disclosure by default; state-by-state consent handling |
| Cost of the human support promise | Tier it (paid plans), use AI triage with human escalation, and measure support cost per customer against margin |
| Finance-integration risk | Approval-gated drafts, Stripe-hosted flows, no custody of funds, audit log |

---

## Sources

- **Voice of customer** (Trustpilot, collected 2026-09-27): [Sintra](https://www.trustpilot.com/review/sintra.ai) · [Motion](https://www.trustpilot.com/review/usemotion.com) · [Polsia](https://www.trustpilot.com/review/polsia.com) · [Manus](https://www.trustpilot.com/review/manus.im) · [Genspark](https://www.trustpilot.com/review/genspark.ai) · [Marblism](https://www.trustpilot.com/review/marblism.com) · [Taskade](https://www.trustpilot.com/review/taskade.com) · [Lindy](https://www.trustpilot.com/review/lindy.ai) · [Durable](https://www.trustpilot.com/review/durable.co)
- **Time and money leakage:** [Stealth Agents](https://stealthagents.com/research/startup-admin-burden-statistics-2026) · [Agility PR](https://www.agilitypr.com/pr-news/pr-news-trends/time-management-new-survey-reveals-biz-owners-spending-time-theyd-rather-spend/) · [Prospeo](https://prospeo.io/s/average-lead-response-time) · [AInora lead response](https://ainora.lt/blog/lead-response-time-statistics-every-study-2026) · [Leadferno](https://leadferno.com/blog/research-website-contact-forms-and-lead-management-uncovering-costly-mistakes) · [Vesma](https://vesma.app/resources/lead-response-time-research) · [AInora missed calls](https://ainora.lt/blog/missed-call-statistics-small-business-2026) · [Aira](https://www.getaira.io/blog/missed-business-calls-statistics) · [QuickBooks late payments](https://quickbooks.intuit.com/r/small-business-data/small-business-late-payments-report-2025/) · [Clockify](https://clockify.me/late-invoice-statistics) · [Picmim](https://blog.picmim.com/blog/how-much-time-companies-spend-social-media) · [Breeze](https://www.breeze.pm/articles/saas-tool-sprawl-statistics) · [QuickBooks 2026 owner report](https://quickbooks.intuit.com/r/small-business-data/business-ownership-in-2026/) · [Booth Associates (NFIB)](https://boothassociatesllc.com/ai-statistics-small-business-2026.html)
- **UX and behavior:** [NN/g articulation barrier](https://www.nngroup.com/articles/ai-articulation-barrier/) · [NN/g State of UX 2026](https://www.nngroup.com/articles/state-of-ux-2026/) · [Approval fatigue](https://tianpan.co/blog/2026/06/25/approval-fatigue-how-human-in-the-loop-gates-decay-into-rubber-stamps) · [TechTarget](https://www.techtarget.com/it-strategy/feature/Human-in-the-loop-shouldnt-rubber-stamp-decisions) · [AARP / NBER self-employment by age](https://www.aarp.org/pri/topics/work-finances-retirement/employers-workforce/older-workers-self-employment/) · [Infobip WhatsApp](https://www.infobip.com/blog/whatsapp-statistics) · [YCloud WhatsApp](https://www.ycloud.com/blog/whatsapp-statistics-for-businesses)
- **Competitors:** [ChatGPT Work](https://thenextweb.com/news/openai-chatgpt-work-agent-launch) · [OpenAI small-business program](https://openai.com/index/introducing-chatgpt-small-business-program/) · [Claude Cowork scheduled tasks](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork) · [Claude Cowork Dispatch](https://support.claude.com/en/articles/13947068-assign-tasks-from-anywhere-in-claude-cowork) · [Genspark Claw](https://www.genspark.ai/genspark-claw) · [Lindy](https://www.lindy.ai/pricing) · [Motion AI SDR](https://www.usemotion.com/ai-employees/ai-sdr) · [Sintra](https://sintra.ai/pricing) · [Marblism](https://www.marblism.com/pricing) · [HoneyBook overview](https://www.softwareadvice.com/crm/honeybook-profile/) · [HoneyBook/Dubsado/Bonsai comparison](https://www.solopad.io/blog/honeybook-vs-dubsado-vs-bonsai) · [PaperclipCloud](https://paperclipcloud.com/) · [Fin outcome pricing](https://fin.ai/pricing)
- **Voice and phone:** [Famulor voice pricing](https://www.famulor.io/blog/ai-voice-agent-pricing-2026-what-10-platforms-actually-cost-per-minute) · [SkipCalls conditional forwarding](https://skipcalls.com/solutions/call-forwarding-setup)
- **This repo:** `packages/db/src/schema/completion_contracts.ts`, `work_assessments.ts`, `decision_training_examples.ts`, `decision_queues.ts`; `doc/DATABASE.md` (decision queues); `doc/SPEC-implementation.md`; `doc/connections/README.md`, `AGENTMAIL.md`, `MEMORY.md`, `FIRST-30-MATRIX.md`; `doc/LOW-TRUST-PRESETS.md`; `ui/src/pages/WhatNeedsMe.tsx`

## Method notes

- **Review coding.** Themes were coded with keyword rules. Precision was checked by reading a random sample of 28 negative reviews; themes were confirmed, but some keyword over-matching remains (for example "trial" counts toward billing). Treat shares as ±5–10 points.
- **Review bias.** Trustpilot skews toward billing grievances, and some five-star reviews are solicited (they name support staff). Lindy's sample is small (40 total reviews).
- **Baselines.** Lead-response, missed-call and late-payment figures mix vendor research and compilations (secondary). The pilot will replace them with our own before-and-after measurements.
- **Estimates.** RICE inputs and person-week estimates are planning estimates; revisit them after the concierge pilot.
