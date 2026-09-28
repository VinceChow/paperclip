# Market Research Report (v2): The Platform for One-Person Companies

**Topic:** Feasibility of a Paperclip-style AI agent orchestration product built for one-person companies ("OPC")
**Target market:** Solo business owners and aspiring founders, including people with little AI knowledge
**End goal under test:** A popular, dead-simple product with great UX, marketed as *the platform for One Person Companies*
**Date:** 2026-09-26 (v2, with full network access)
**Companion documents:**
- [Industry kits: templates for consultants, coaches, designers, property agents, creators](./industry-kits.md)
- [Reliability and cost: the outcome loop harness](./reliability-cost-harness.md)
- [Go-to-market and marketing plan: landing page, social media, launch](./marketing-plan.md)
- [Product feature strategy (CPO): what to build, 10–100x targets, backlog and roadmap](./product-feature-strategy.md)
- [Product requirements document (PRD): from-scratch build spec](./prd.md)

**Method:** Primary data where it exists: the US Census 2023 Nonemployer Statistics file, Census business-formation releases, Google Trends, domain registries (RDAP), the USPTO trademark search, and competitor pricing pages rendered in a headless browser. Secondary data (industry reports, press, reviews) is marked as such. See [What changed since v1](#what-changed-since-v1) and [Data quality notes](#data-quality-notes).

---

## Executive Summary

**Verdict: Go.** Demand is strong and people already pay for this. Market it as the platform for One Person Companies, but use "One Person Company" as the *category you lead*, not as your trademarked brand name. Win on proven outcomes and trust, not on autonomy.

1. **Demand is large and verified.**
   - The US had **30.43M nonemployer businesses in 2023**, with **$1.75T in receipts** (Census primary file).
   - **7.46M** of them earn ≥$50K a year, so they can pay for software.
   - Across the 13 knowledge-service segments this product fits, there are **7.45M solo businesses**, of which **1.63M earn ≥$50K**.
   - Korea counts **1.16M "one-person creative enterprises"** (+15.4% YoY).
   - **23 Chinese cities** have run formal OPC support programs since October 2025.
2. **"One Person Company" is a rising term that no one owns in the West.**
   - Worldwide Google search interest for the phrase rose about **2.5x** from 2024 to Q2 2026.
   - Its top related searches are *definitional* ("what is one person company"): people are still learning what it means, which is a category-creation opening.
   - The alternative term "solopreneur" is being claimed by incumbents. Its #1 related search is Intuit's *QuickBooks Solopreneur* product.
   - Caveats: "OPC" collides with the OPC Foundation's registered marks, "onepersoncompany.com" has been taken since 2012, and a wave of OPC-style `.ai` domains was registered in 2025–26.
3. **The market gap is outcomes and trust, not capability.**
   - The "autonomous company" leaders sell activity: 206 of 30,272 NanoCorp companies (0.68%) had ever earned anything as of July 2026. Polsia's reviews are split between 5 stars and 1 star.
   - AI-employee bundles (Sintra, Marblism) sell help with individual tasks, not coordinated work toward a goal.
   - Orchestration tools (Paperclip, n8n, Relevance) are still too technical for this buyer.
   - 78% of small-business owners don't trust AI with even low-level tasks without oversight.
   - **No product promises and verifies "done" for solo businesses.**
4. **Industry kits (templates) are a strong multiplier for demand, but they should sit inside one product rather than become separate products.**
   - Template libraries drive adoption: n8n has 11.7K+ workflow templates, 69% of them AI; Notion is known for starter templates; PaperclipCloud sells "AI company templates."
   - Per-industry search demand is small next to "AI for small business" (~48 vs 2–7 on the same Google Trends scale).
   - So: one horizontal OPC brand, with industry kits as the onboarding path and as landing pages. See the [kits document](./industry-kits.md).
5. **Reliability and cost are solvable with harness engineering. This is the moat.**
   - Model the product as workflows with an "outcome contract" (a definition of done), not as an org chart of always-on agents.
   - At current Claude prices, a well-designed active user costs **about $31–40/month** in inference.
   - The same work costs about **$114** on a single frontier model without caching.
   - Paperclip-style timed heartbeats (5 agents every 30 minutes) cost about **$980**.
   - See the [reliability and cost document](./reliability-cost-harness.md).
6. **UX is the product.** Users see a team, a "Needs you" inbox, a definition of done and a Friday results report. They never see agents, adapters, tokens or heartbeats. See [§6.4](#64-product-and-ux-dead-simple-for-people-with-no-ai-knowledge).
7. **Go-to-market is category-led and founder-led.** Channels: a public "Company of One, Run in Public" content series, an OPC community, industry creators and affiliates, SEO on "what is a one-person company," and one launch moment per kit. Paid acquisition stays off until conversion is proven. Base target: 4,000 paying companies in 12 months at a blended CAC ≤ $200. See the [marketing plan](./marketing-plan.md).

### Scorecard

| Dimension | Rating | Evidence |
|---|---|---|
| Market demand | **Strong** | 30.4M US nonemployers; 1.16M Korean one-person enterprises; China OPC policy wave; record-pace business formation |
| Willingness to pay | **Proven at $24–$99/mo** | Marblism $24; Sintra $97 list price; Lindy $29.99–$199.99; Motion AI Employees $99–$599; Lofty $299 for solo real estate agents |
| "One Person Company" as positioning | **Feasible as a category, weak as a brand name** | Rising, unowned, meaningful across regions; generic, hard to trademark; "OPC" conflicts with an existing mark |
| Technical feasibility | **High** | Paperclip is MIT-licensed and already has budgets, approvals, completion reviews, a watchdog, recovery, evals and a connection catalog |
| Reliability at acceptable cost | **Medium → High with the right harness** | Measured levers: caching 2.7–5.3x cheaper; retrying failures at higher effort cuts cost about 45%; independent grading loops |
| Competitive intensity | **High** | Polsia ($30M raised), NanoCorp, Sintra, Marblism, Motion, Lindy; OpenAI ChatGPT Work plus its small-business program; Claude Cowork; Lofty |
| Regulatory / reputational risk | **Medium** | FTC Operation AI Comply targets "AI business opportunity" claims; EU AI Act Article 50 in force since 2026-08-02 |

---

## What changed since v1

| Item | v1 (search summaries) | v2 (verified) |
|---|---|---|
| US nonemployers | 30.4M (secondary) | **30,427,808 establishments, $1.753T receipts (2023)**, from the Census NES file |
| Share of nonemployers that can pay | Not measured | **24.5% earn ≥$50K; 13.2% earn ≥$100K; 60.6% earn <$25K** |
| Polsia Trustpilot | 1.8/5 on 35 reviews | **3.2/5 on 279 reviews**, sharply split: 33% five-star, 35% one-star |
| NanoCorp outcomes | "<1% earned" | **206 of 30,272 companies ever earned** (July 20, 2026 update); **$1,530 earned platform-wide in 30 days** (Sept 15, 2026) |
| Lindy pricing | $49.99+ | **$29.99 / $99.99 / $199.99 per user**; "approvals built in"; pauses when credits run out |
| Paperclip positioning | "Zero-human companies" | Homepage now reads **"A team of agents for every person."** Upstream is moving toward mainstream users. |
| Paperclip hosting wrappers | Demand signal | Demand is real but thin: **Paperclip.inc shuts down on 2026-10-02**; PaperclipCloud's banner promotes a different product |
| Polsia revenue | ~$10M ARR (self-reported) | Fortune (March 2026): **$4.5M run-rate**; later self-reports ~$10M. Treat as unverified. |

---

## 1. Market Overview

| Metric | Value | Source |
|---|---|---|
| US nonemployer businesses (2023) | **30,427,808**; receipts **$1.753T** | [Census NES 2023 file](https://www2.census.gov/programs-surveys/nonemployer-statistics/datasets/2023/historical-datasets/) |
| …with receipts ≥ $25K / ≥ $50K / ≥ $100K | **11.99M / 7.46M / 4.03M** | Same (receipts-size classes) |
| Legal form | 26.3M sole proprietors; 2.3M partnerships; 1.4M S-corps; 0.46M C-corps | Same |
| Nonemployers in 13 target knowledge-service segments | **7.45M** (1.63M earn ≥$50K) | Same; see §3 |
| US independent workers (2025) | 72.9M total; **27.6M full-time** | [MBO Partners](https://www.mbopartners.com/state-of-independence) |
| Skilled US knowledge workers who freelance | **38% in 2026** (28% in 2025) | [Upwork Future Workforce Index 2026](https://investors.upwork.com/news-releases/news-release-details/upworks-future-workforce-index-2026-how-ai-redefining-value-work) |
| Solo-founder share of new startups | 23.7% (2019) → **36.3% (H1 2025)** | [Carta](https://carta.com/data/solo-founders-report/) (via press; carta.com blocks automated fetches) |
| Time to first revenue | **20%** of Stripe Atlas startups charge a customer within 30 days (more than double 2020); 42% build AI products; 44% of those build agents | [Stripe Atlas 2025 review](https://stripe.com/blog/stripe-atlas-startups-in-2025-year-in-review) |
| Korea one-person creative enterprises | **1.16M** (+15.4% YoY; 23.7% of all startups) | [Korea policy briefing](https://www.korea.kr/briefing/pressReleaseView.do?newsId=156753709), [Newspim](https://www.newspim.com/news/view/20260406000315) |
| China OPC | 23 major cities with OPC programs since Oct 2025; >7M new solo companies last year (+42%); youth unemployment 18.9% | [Rest of World](https://restofworld.org/2026/china-ai-one-person-companies-incentives/), [Honghub report](https://www.globenewswire.com/news-release/2026/04/29/3283960/0/en/Honghub-Unveils-2026-OPC-Insight-Report-Revealing-China-s-One-Person-Company-Boom-and-a-72x-AI-Labor-Advantage.html), [Asia Financial](https://www.asiafinancial.com/chinas-young-tapping-ai-subsidies-to-launch-one-person-firms) |
| China OPC founder profile | 75% non-technical; **median AI spend $39/mo**; top 20% spend $200+/mo | Honghub 2026 OPC Insight Report (1,500+ surveys) |
| AI agents market (mostly enterprise) | $10.9B–$19.3B in 2026; ~40–50% CAGR | [Grand View](https://www.grandviewresearch.com/industry-analysis/ai-agents-market-report), [MarketsandMarkets](https://www.marketsandmarkets.com/Market-Reports/agentic-ai-market-208190735.html) |

### Industry context

**One-person companies are a global movement, and each market frames them differently:**
- **US / UK:** "solopreneur," "freelancer," and "one-person business."
- **India:** a *legal entity*. The One Person Company was created by the Companies Act 2013, with tens of thousands registered.
- **Korea:** a *policy category*, the one-person creative enterprise under the 1인 창조기업 support act.
- **China:** a *state-backed movement*, with OPC communities, compute subsidies and loans. In all three Asian markets, a significant part of the push comes from weak job markets for young people.

**AI is turning "solo" from a lifestyle into a company structure.** Founders now use agents to cover roles they would once have hired for. Stripe says 44% of its AI-focused startups are building agents. Upwork describes an emerging role it calls the "AI orchestrator."

**Big platforms are moving in:**
- OpenAI launched ChatGPT Work on 2026-07-09 and a small-business program on 2026-07-21, with Shopify, Intuit and Wix partners ([OpenAI](https://openai.com/index/introducing-chatgpt-small-business-program/)).
- Anthropic's Claude Cowork reached web and mobile in July ([TechCrunch](https://techcrunch.com/2026/07/07/the-coding-agent-wars-are-spilling-into-the-rest-of-the-office-claude-cowork/)).
- Upstream Paperclip now pitches "a team of agents for every person" ([paperclip.ing](https://paperclip.ing/)).

**Capability is climbing fast, but reliability lags:**
- METR measures the length of tasks agents can finish with 50% success doubling roughly every 4–7 months ([METR](https://metr.org/time-horizons/)).
- Consistency is weaker than one-off success. On τ-bench, pass^8 (succeeding on all 8 of 8 tries) fell about 60% below pass^1 ([Sierra](https://sierra.ai/blog/benchmarking-ai-agents)).
- Gartner expects more than 40% of agentic AI projects to be canceled by 2027 ([Gartner](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027)).
- **Implication:** the product that makes agents *dependable* for non-experts wins, not the one that makes them most autonomous.

### Market sizing (estimates; assumptions stated)

| Layer | Definition | Math | Size |
|---|---|---|---|
| **TAM (US)** | All US nonemployers at an AI-operations budget | 30.4M × $600/yr | ≈ **$18B/yr** |
| **SAM (US)** | Solo businesses in the 13 knowledge-service segments | 7.45M × $600/yr | ≈ **$4.5B/yr** |
| **Core SAM (US)** | Segment businesses earning ≥$50K a year (the buyers who pay) | 1.63M × $948/yr ($79/mo) | ≈ **$1.5B/yr** |
| **SOM (3–5 yrs)** | Realistic paid share, global | 100K–250K paying × ~$700/yr | ≈ **$70M–$175M ARR** |

The SOM rests on comparable companies:
- Sintra reached ~40K paying customers and ~$12M ARR within 12 months ([Tech.eu](https://tech.eu/2025/06/10/lithuanian-ai-startup-sintra-secures-17m-seed-empowering-smbs-with-ai-helpers/)).
- Marblism claims 40,000+ businesses.
- Polsia reports about 7.6K customers in about 5 months.

International markets (UK, EU, India, Korea, Southeast Asia) could plausibly add 1–2x the US SAM; China is largely closed to foreign software. All sizing figures are order-of-magnitude estimates, not forecasts.

---

## 2. Positioning: "The Platform for One Person Companies". Is it feasible?

### 2.1 Search demand (Google Trends, pulled 2026-09-26)

**Worldwide interest by quarter** (same scale across terms; 100 = peak):

| Quarter | "one person company" | "one person business" | "solopreneur" |
|---|---|---|---|
| Q1 2024 | 2.2 | 1.9 | 0.2 |
| Q1 2025 | 2.2 | 2.1 | 1.0 |
| Q3 2025 | 2.8 | 2.5 | 1.1 |
| Q1 2026 | 4.4 | 4.1 | 1.4 |
| Q2 2026 | **5.4** | **4.8** | **2.1** |
| Q3 2026 (partial) | 3.8 | 3.1 | 1.1 |

The Q3 2026 row covers only part of the quarter, and every term tracked (including "AI agents") dipped by a similar amount. Read it as noise, not a reversal.

**United States:** "one person company" searches outnumber "solopreneur" searches by roughly 4–7x, and "one person company" rose from ~46 to ~85 (Q4 2023 → Q2 2026).

**Top countries for "one person company" (last 12 months):** US 100, UAE 93, Singapore 68, Ethiopia 68, India 51, Kenya 48, South Africa 46, South Korea 46, Nigeria 44, Philippines 42, China 40, UK 35.

**What people search for:**

| Term | Top related queries |
|---|---|
| "one person company" | "what is one person company" (100), "meaning" (14), "in India" (13), "examples" (8), "registration" (6) |
| "solopreneur" | "quickbooks" (100), "quickbooks solopreneur" (99), "what is solopreneur" (65), "the ai solopreneur" (48, rising) |

What this tells us:
- ✅ **The term is growing, international, and nobody commercial owns it.** People are still asking what it *means*. A company that defines it through content, a yearly "State of One-Person Companies" report and a community can own the category.
- ✅ **"Company" signals ambition and legitimacy** ("I run a company"), and it fits the agent-team idea naturally: you are the CEO, and the agents are your team. It is also Paperclip's own mental model.
- ⚠️ **In India, OPC is a legal entity type.** There, a lot of search traffic is people looking to *register* an OPC (legal-services intent), and SEO competition comes from registration firms. This can also be an opportunity: registered OPC owners are a precise target group to partner on.
- ⚠️ **"Solopreneur" is being claimed by incumbents.** Intuit's QuickBooks Solopreneur dominates its related searches. That is another reason to lead with "One Person Company" rather than "solopreneur."

### 2.2 Naming, trademark and domains

| Check | Finding | Implication |
|---|---|---|
| USPTO search for "one person company" | **No live or dead marks found** ([tmsearch.uspto.gov](https://tmsearch.uspto.gov/search/search-results?query=%22one%20person%20company%22&section=default)) | Available, but a descriptive or generic phrase is likely to be refused registration. You can *use* it; you probably can't *own* it. |
| "OPC" | The OPC Foundation holds registered "OPC" / "OPC UA" marks for industrial-automation software ([OPC Foundation](https://opcfoundation.org/terms-and-conditions/)) | Don't make "OPC" the product's brand. Use it only as shorthand for the category. |
| India | "One Person Company" is a statutory entity type ([MCA](https://www.mca.gov.in/content/mca/global/en/help-faq/faqs/company-services/incorporation/one-person-company.html)) | Generic in India. Use carefully in copy; never imply legal incorporation services unless you offer them. |
| Domains (RDAP, 2026-09-26) | `onepersoncompany.com` registered 2012; `opc.com` 1994; `opc.ai` 2018; `companyofone.ai` 2025; **`myopc.ai` Feb 2026, `onepersonco.ai` Apr 2026, `oneperson.ai` May 2026**; `onepersoncompany.co` and `.io` returned no registration record (possibly available; .ai lookups for the exact phrase were rate-limited) | Others started claiming this vocabulary in 2026. That confirms the trend and means category terms won't make a distinctive brand. |
| Related concept | "Company of One" is the title of Paul Jarvis's 2019 book | Avoid it as a name. It works as a cultural reference. |

### 2.3 Recommendation

- **Own the category, brand the product.** Pattern: **"[Distinct brand]: the platform for one-person companies."** Build category assets:
  - A yearly *State of One-Person Companies* report. The Census NES analysis in this document is a starter dataset.
  - An OPC founder community with public "company pages."
  - Industry kits.
  - A public outcomes index that shares real, anonymized results.
- **Localize the phrase:**

  | Market | Phrasing |
  |---|---|
  | US / UK | "one-person company" and "one-person business" |
  | India | "one-person company", with care around the legal meaning |
  | Korea | "1인 기업" |
  | Mandarin-speaking diaspora and Southeast Asia | "OPC" is recognized from Chinese media |

- **Never sell income.** The category sits next to the "AI passive income" schemes the FTC shut down under Operation AI Comply (Click Profit; Ascend Ecom, at least $25M in losses; FBA Machine, about $15M) ([FTC](https://www.ftc.gov/news-events/news/press-releases/2025/03/ftc-acts-stop-click-profit-online-business-opportunity-has-cost-consumers-least-14-million), [Benesch](https://www.beneschlaw.com/insight/one-year-in-ftcs-operation-ai-comply-continues-under-new-administration-signaling-enduring-enforcement-focus/)). Position it as "run your company like a team of ten," never "earn while you sleep." Polsia's headline is literally "AI That Runs Your Company While You Sleep."

---

## 3. Target Market

### 3.1 US segment sizing (Census NES 2023; primary data)

| Segment | NAICS | Nonemployers | Avg receipts | ≥ $25K | ≥ $50K (share) |
|---|---|---|---|---|---|
| Consultants (management, scientific, technical) | 5416 | 1,081,961 | $59.8K | 442,474 | 284,442 (26%) |
| Property agents & brokers | 5312 | 824,003 | $63.6K | 436,678 | 279,718 (34%) |
| Designers (graphic, interior, other) | 5414 | 277,731 | $46.1K | 98,172 | 59,084 (21%) |
| Creators (independent artists, writers, performers) | 7115 | 1,088,020 | $31.0K | 253,818 | 127,906 (12%) |
| Marketing, advertising and PR freelancers | 5418 | 207,863 | $60.8K | 82,944 | 53,175 (26%) |
| IT and software freelancers | 5415 | 343,329 | $60.0K | 144,880 | 95,641 (28%) |
| Bookkeepers, accountants, tax preparers | 5412 | 396,812 | $34.5K | 130,959 | 71,908 (18%) |
| Photographers | 54192 | 236,666 | $28.8K | 73,093 | 39,121 (17%) |
| Therapists and counselors | 62133 | 226,306 | $56.1K | 129,551 | 88,138 (39%) |
| Lawyers (solo) | 5411 | 274,000 | $84.5K | 147,901 | 106,824 (39%) |
| Tutors and instructors | 611 | 893,520 | $18.3K | 149,553 | 69,241 (8%) |
| Other personal services (includes many coaches) | 81299 | 755,943 | $36.0K | 214,124 | 113,344 (15%) |
| All other professional services | 54199 | 841,723 | $69.4K | 366,293 | 239,789 (28%) |
| **Total, 13 segments** | | **7,447,877** | **$47.7K** | **2,670,440** | **1,628,331** |

Coaches don't have their own NAICS code. They are spread across 5416, 611 and 81299. The ICF counts **122,974 coach practitioners worldwide** with $5.34B in revenue, and only **6%** use AI coaching tools today ([ICF 2025](https://coachingfederation.org/blog/coaching-industry-continues-global-growth-with-5-34-billion-usd-revenue-new-research-reveals/)).

For creators, Goldman Sachs estimates **50M creators globally**. About half earn under $15K a year and about 4% earn over $100K ([Goldman Sachs](https://www.goldmansachs.com/insights/articles/the-creator-economy-could-approach-half-a-trillion-dollars-by-2027)).

For property agents, NAR had **1.44M members** as of June 2026. Nearly half use AI daily (23%) or weekly (25%), and 81% adopt technology mainly to save time ([NAR](https://www.nar.realtor/newsroom/realtors-adopt-technology-to-save-time-and-improve-the-client-experience-nar-report-finds)).

### 3.2 Who to serve first

| Group | Size (US) | Pay ability | Pain intensity | Fit | Priority |
|---|---|---|---|---|---|
| **Established OPC operators**: ≥$50K receipts, knowledge services | ~1.6M in target segments | High | High (time; inconsistent marketing and follow-up) | Recurring, checkable workflows | **1: beachhead** |
| **Growing operators**: $25–50K, want to reach full-time | ~1.0M in target segments | Medium | Very high (pipeline) | Growth kits: leads, content | 2 |
| **Aspiring founders**: idea stage | Near-record business applications | Low | High (overwhelm) | Guided launch with demand checks | 3: acquisition funnel |
| **Side hustlers / occasional independents** | 37.4M (MBO) | Low | Medium | Light plan | 4 |
| **International OPC** (India legal OPCs, Korea 1인 기업, Southeast Asia) | 1.16M Korea; tens of thousands of India OPCs | Medium | High | Messaging-first; localized kits | Expansion |

### 3.3 Primary personas

| Persona | Snapshot | Jobs to be done | What they'll pay for |
|---|---|---|---|
| **Maya, the independent consultant** | 41, ex-corporate, $120K receipts, 3–5 clients | Keep pipeline warm, publish thought leadership, prepare proposals, invoice and follow up | Pipeline that doesn't depend on her memory; proposals in her voice |
| **Leo, the property agent** | 35, 18 deals a year, leads from portals | Respond to leads in minutes, launch listings, run nurture drips, stay compliant | Speed-to-lead; listing launch kit; never missing a follow-up |
| **Ana, the coach / creator** | 33, 12K followers, $60K from programs | Weekly content across platforms, community replies, launch calendar, client onboarding | Consistent content without burnout; launches that run on time |

What all three share: they are **non-technical, short on time, protective of their reputation, and want to approve anything that goes out.** They measure value in *hours saved and clients won*, not in AI features.

---

## 4. Competitive Landscape (verified 2026-09-26)

| Competitor | Category | Pricing (verified) | Strengths | Weaknesses |
|---|---|---|---|---|
| **Polsia** | Autonomous company launcher | $49/mo + 20% revenue share (press); "free to start" (site) | Strong story ("Polsia is your first employee"); $30M raised at ~$250M valuation ([AIN](https://en.ain.ua/2026/05/25/ai-startup-polsia-with-no-employees-raised-30m-in-funding/)) | Trustpilot 3.2/5 on 279 reviews, 35% one-star; complaints about credits, broken sites, domain lock-in ([Trustpilot](https://www.trustpilot.com/review/polsia.com)); "while you sleep" framing |
| **NanoCorp** (YC) | Autonomous company launcher | $30/mo for 30 credits + **20% withdrawal fee** ([pricing](https://www.nanocorp.so/pricing)) | Transparent public leaderboard; "no human in the loop" | 206 of 30,272 companies ever earned; $1,530 earned platform-wide in 30 days ([preuve.ai](https://preuve.ai/blog/nanocorp-review)) |
| **Sintra** | AI-employee bundle | $97/mo list; $15.60–$48.50 on promotion; 250 credits ([pricing](https://sintra.ai/pricing)) | 12 named helpers; "zero technical setup"; ~40K paying customers | Chat-and-draft help; credit caps; runs on a single model |
| **Marblism** | AI-employee bundle | **$24/mo** for 7 "employees" and 50 hours of work ([pricing](https://www.marblism.com/pricing)) | Cheapest; claims 40K+ businesses; receptionist and website included | Shallow orchestration; output-quality risk |
| **Lindy** | Assistant / agent builder | $29.99 / $99.99 / $199.99 per user ([pricing](https://www.lindy.ai/pricing)) | Approvals built in; pauses when credits run out; iMessage; SOC 2 | Credit meter; built around teams and Slack |
| **Motion** | Agentic work suite | $19–$29/seat; AI Employees $99–$599/mo | $60M at $550M valuation; AI Employees went from $0 to 8-figure ARR in 3 months ([Motion](https://www.usemotion.com/blog/motion-raises-60m-to-build-the-agentic-work-suite-for-businesses)) | Built for small teams, not solo owners; pricing complaints |
| **Taskade Genesis** | "One-person company" workspace | Free; Pro $10/mo annual; up to $250 | Explicitly targets the one-person-company idea ([Taskade](https://www.taskade.com/blog/one-person-companies)) | A workspace or builder, not outcome-verified operations |
| **Paperclip** (upstream, MIT) | Open-source orchestration | Free; hosted wrappers ~$12–$69/mo | 74K+ stars (per its site); budgets, governance; now "a team of agents for every person" | Self-hosted and technical; hosting wrappers struggling (Paperclip.inc closing 2026-10-02) |
| **Lofty** | Vertical: real estate | **$299/mo** for solo agents | "Agentic OS" for real estate: lead, social and seller agents ([Ascendix](https://ascendix.com/blog/ai-real-estate-agents/)) | Expensive; one vertical only |
| **Coachvox / Delphi** | Vertical: coaches and creators | $99/mo + **10%** (Coachvox); $99–$349 + **15%** (Delphi) | AI clones of the expert for their audience ([Personify](https://personify.fyi/blog/ai-clone-cost/)) | Revenue share; clone only, doesn't run the business |
| **OpenAI ChatGPT Work** + small-business program | Platform | Bundled | Huge distribution; partners Shopify, Intuit, Wix; free training | General-purpose; no structure for running a company |
| **Claude Cowork** | Platform | Claude plans | Strong agent quality | Task- and file-oriented, not a company operating layer |

### 4.1 Market-gap matrix

Legend: ✅ strong · ◐ partial · ❌ missing.

| Capability a non-technical OPC needs | Launchers (Polsia, NanoCorp) | AI-employee bundles (Sintra, Marblism) | Builders (Lindy, Relevance, n8n) | Paperclip OSS | Platforms (ChatGPT Work, Cowork) | Vertical AI (Lofty, Coachvox) | **Target product** |
|---|---|---|---|---|---|---|---|
| Dead-simple, no setup | ✅ | ✅ | ◐ | ❌ | ✅ | ◐ | ✅ |
| Coordinated multi-step work toward a goal | ◐ | ❌ | ◐ | ✅ | ◐ | ◐ | ✅ |
| **Verified "done"** (definition of done, checks, grader) | ❌ | ❌ | ❌ | ◐ (completion reviews, watchdog) | ◐ | ❌ | ✅ |
| **Approvals by default** for outward actions | ❌ (no human in loop) | ◐ | ✅ | ✅ | ◐ | ◐ | ✅ |
| Predictable flat price (no token or credit anxiety) | ◐ | ◐ (credits) | ❌ (credits) | ❌ (tokens) | ✅ | ✅ | ✅ |
| **No revenue share** | ❌ (20%) | ✅ | ✅ | ✅ | ✅ | ◐ (10–15% for coaches) | ✅ |
| Industry workflows (not generic roles) | ❌ | ◐ (role-based) | ◐ (templates) | ◐ (ClipHub concept) | ❌ | ✅ (single vertical) | ✅ (kits) |
| **Honest outcome reporting** | ◐ (NanoCorp leaderboard) | ❌ | ❌ | ◐ (costs) | ❌ | ◐ | ✅ |
| Ownership and portability of assets and data | ❌ (lock-in complaints) | ◐ | ◐ | ✅ | ◐ | ◐ | ✅ |

### 4.2 The six gaps

1. **Outcome gap.** Everyone sells *activity* ("AI employees work 24/7"), and nobody guarantees *done*. The clearest evidence is NanoCorp's 0.68% ever-earned rate.
2. **Trust gap.** 78% of small-business owners don't fully trust AI even with low-level tasks without oversight ([KVIA/Stacker](https://kvia.com/stacker-small-business/2026/07/16/3-4-of-small-businesses-dont-trust-ai-for-basic-tasks/)). Meanwhile the launchers advertise "no human in the loop."
3. **Orchestration gap for non-experts.** Bundles give you helpers that don't coordinate with each other. Coordination tools are built for developers.
4. **Economics gap.** Customers face revenue shares (Polsia 20%, NanoCorp 20%, Coachvox 10%, Delphi 15%), credit meters (Lindy, Sintra, Motion) and surprise token bills (Paperclip self-hosting).
5. **Vertical gap.** Horizontal tools are organized around generic *roles* ("social media manager"). Real work is organized around *industry workflows* ("listing launch," "client onboarding"). Vertical tools that do exist cost a lot (Lofty $299) or cover one narrow job (clones).
6. **Identity gap.** No Western platform owns "One Person Company" as a category and community. China's OPC communities show there is demand for the *belonging* side, not just the tooling.

---

## 5. Opportunities

| # | Opportunity | Size | Competition | Feasibility | Priority |
|---|---|---|---|---|---|
| 1 | **OPC operating platform for established operators**: industry kits, outcome-verified workflows, approvals, flat price | High | Medium | High | **1** |
| 2 | **OPC category and community**: yearly report, public founder pages, templates marketplace (ClipHub-style) | Medium (brand and acquisition) | Low | High | **2** |
| 3 | **Guided "honest launch"** for aspiring founders: demand check → offer → first customer | High (funnel) | High | Medium | 3 |
| 4 | **Messaging-first OPC** (iMessage, WhatsApp, Telegram approvals and briefs) for mobile-first markets | Medium–High | Low | Medium (repo has an experimental iMessage channel) | 3 |
| 5 | **Partnerships**: India OPC registration services, Korean support centers, Shopify/Wix app stores, coaching schools, brokerages | Medium | Low | Medium | 4 |

**Recommended focus:** Opportunity 1, with Opportunity 2 running in parallel as the brand engine:
- Start with **four kits: Consultant, Coach, Creator, and Creative freelancer (designer/marketer).** Coach and Creator share one content engine, so this is about three engines of build work. These segments are digital, low-compliance and high-frequency.
- Add **Property agent** next. The pain is strong and willingness to pay is proven (Lofty), but it needs TCPA and Fair Housing guardrails.
- Details in the [kits document](./industry-kits.md).

---

## 6. Feasibility

### 6.1 Technical: High (build on Paperclip, but change the abstraction)

Paperclip already provides the hard infrastructure:
- Goal → task hierarchy.
- Budgets with hard stops.
- Approvals ("Ask first").
- **Native completion reviews** (a reviewer agent accepts or rejects the work).
- A **task watchdog** that restarts wrongly stopped work.
- **Recovery** with a three-attempt incident budget.
- Durable continuation envelopes.
- Eval families.
- A connection catalog (Gmail, Google Workspace, Slack and others).
- Agent Chat, and an experimental iMessage channel.
- A templates concept (ClipHub / teams catalog).

See `doc/execution-semantics.md`, `doc/TASK-WATCHDOG.md`, `doc/plans/2026-09-08-reliable-execution-recovery.md` and `doc/CLIPHUB.md`.

**The needed change:** replace the *org chart of always-on agents with heartbeats* with **outcome-driven workflows triggered by events**, presented to the user as a team. That is both cheaper (§6.2) and more reliable. The full design, including a map from existing Paperclip features to gaps, is in the [reliability and cost document](./reliability-cost-harness.md).

### 6.2 Unit economics: viable at $49–$79 per month

Modeled with current Claude API list prices: Haiku 4.5 $1/$5, Sonnet 5 $2/$10, Opus 5.5 $4/$20 per million input/output tokens. Cache reads cost 0.1x the input price (0.05x on Opus 5.5); batch is 50% off ([Anthropic pricing](https://platform.claude.com/docs/en/about-claude/pricing)). The workload is one active OPC user per month: 30 daily briefs, 900 email classifications, 150 reply drafts, 13 long-form content pieces, 80 lead-research tasks, 4 weekly reports, and 260 grader passes.

| Design | Inference $/user/month |
|---|---|
| **Routed models + prompt caching + event triggers** (recommended) | **≈ $31** (≈ $39 with a 25% allowance for revisions and retries) |
| Routed models, no caching | ≈ $69 |
| Everything on the frontier model, no caching | ≈ $114 |
| Timed heartbeats: 5 agents every 3 hours | ≈ $163 |
| Timed heartbeats: 5 agents every 30 minutes | **≈ $980** |

At $79/mo, the recommended design leaves about a 40–50% gross margin for an *active* user after infrastructure (~$5) and payment fees (~3%). Lighter users cost far less. Two things push margins up over time: model prices at constant capability are falling about 10x a year ([Epoch AI](https://epoch.ai/data-insights/llm-inference-price-trends)), and newer models are cheaper per *solved* task (Sonnet 4.6 → 5 was 15% cheaper per solved task).

### 6.3 Pricing recommendation

| Plan | Price | Includes |
|---|---|---|
| Solo | $29/mo | 1 kit, core workflows, drafts plus approvals, light allowance (no web research) |
| **Company** | **$79/mo** | All kits for your industry, research and leads, auto-mode on the trust ladder, messaging channels |
| Company+ | $199/mo | Multiple brands, higher caps, priority models, custom kit |

No revenue share, 14-day trial, and annual discount. Allowances are shown in dollars and in "jobs," never in tokens or credits.

### 6.4 Product and UX: dead simple for people with no AI knowledge

Paperclip's own product goals already point this way: "time-to-first-success under 5 minutes," "progressive disclosure," and "do not force users to understand provider/API-key plumbing" (`doc/PRODUCT.md`). An OPC product has to go further, because the user has never configured an agent and never will.

**What the user sees instead of Paperclip concepts**

| Paperclip concept | What a non-technical OPC owner sees |
|---|---|
| Company + goal | "My business" + "This month's goal" (for example *5 new clients*) |
| CEO agent + org chart | A **team card** per kit (Chief of Staff plus 3–4 teammates). No org chart unless asked. |
| Adapters (Claude Code, Codex, OpenClaw…) | Nothing. Models are bundled and routed automatically. |
| Heartbeats | "Works when a new email, lead or meeting arrives" · "Sends your brief at 8am" |
| Issues / sub-issues | **This week's plan**: a checklist that expands on tap |
| Outcome contract | **"Done means…"** card on every job, with ✓ marks as checks pass |
| Budgets (token salaries) | "You've used $18 of your $40 this month" (never tokens or credits) |
| Approvals / board | **Needs you** inbox: Approve · Edit · Skip, one tap on a phone, email, iMessage or WhatsApp |
| Work products | **Results** gallery: posts, proposals, invoices, pages |
| Connections catalog | "Connect Gmail" with plain-language scopes ("read and draft; never send without your OK") |
| Run transcripts / logs | "What happened and why" in two sentences; raw logs three taps deep |

**Principles**
1. **Five-minute start.**
   - The user answers a short interview: offer, ideal client, prices, and a website URL or voice samples.
   - The user picks a kit, and the first job runs live while they watch.
   - Target: the first *accepted* deliverable within 10 minutes.
2. **Zero setup.** No API keys, no model choice, no prompt writing. Industry defaults come from the kit.
3. **One place to act.** Everything that needs the owner lands in the Needs-you inbox. It works on mobile first and is also available by email or messaging app.
4. **Visible trust ladder.** Each action type (for example "send follow-up emails") shows its level: *Draft only → Ask me → Auto with daily digest*. The product *suggests* promotion after a streak of approvals with no edits. It never promotes on its own for actions that move money or can't be undone.
5. **Undo and recall.** Sends are delayed for a short window ("undo send"), scheduled posts can be cancelled, and every action shows *why* it happened.
6. **Plain-language money.** Allowances are shown in dollars and jobs, with hard caps. Nothing surprises the user on the bill.
7. **Friday results report.** It covers what got done, estimated hours saved, cost, **what didn't work**, and next week's plan. It is also the retention and sharing moment.
8. **Progressive disclosure.** Summary → steps and checks → raw logs, for the curious.
9. **Accessible and local.** WCAG 2.2 AA. Kits and UI are localized for expansion markets (Korean; English/Hindi for India).

**UX metrics:**
- Time to first accepted deliverable (target < 10 minutes).
- Onboarding completion (target ≥ 70%).
- Approvals handled on mobile (share).
- Support tickets per active company.
- Weekly active approvers.
- CSAT after the weekly report.

---

## 7. Risks & Challenges

| Risk | Impact | Likelihood | Mitigation |
|---|---|---|---|
| Platforms bundle "good enough" agents (OpenAI small-business program, Cowork, Shopify, Intuit) | High | High | Own the operating layer and the category: kits, outcome contracts, approvals, business memory, community. Integrate with the platforms rather than compete with them. |
| Outcome gap and churn (AI apps churn 30% faster; [RevenueCat](https://techcrunch.com/2026/03/10/ai-powered-apps-struggle-with-long-term-retention-new-report-shows)) | High | High | Outcome contracts, first-pass acceptance metric, weekly results report, kits built around recurring jobs |
| Reliability and consistency (pass^k drop; 30% on realistic office tasks) | High | Medium (falling) | Outcome loop: checks, independent grader, human approval; narrow scopes; regression evals per kit |
| Category association with "AI passive income" schemes | High | Medium | No income claims; FTC-reviewed copy; publish honest outcomes |
| Trademark weakness of "One Person Company" / "OPC" conflict | Medium | High | Distinct brand plus a category descriptor; don't brand as "OPC" |
| EU AI Act Article 50 (disclosing AI to people; marking synthetic content) since 2026-08-02; CAN-SPAM, TCPA, Fair Housing in verticals | Medium | High | AI disclosure by default in customer-facing messages; content marking; compliance guardrails in each kit |
| Cost blowouts (heartbeat or loop sprawl) | Medium | Medium | Event triggers, caching, routing, hard dollar caps per job and per month |
| Upstream Paperclip heading to the same audience | Medium | Medium | Loose coupling; contribute upstream; stay distinct as the OPC-specific, kit-driven product |
| Segment economics (60.6% of nonemployers earn <$25K) | Medium | High | Target the ≥$50K operators first; low-cost Solo plan; annual pricing |

---

## 8. Recommended Next Steps

### Phase 0: Validate (3–4 weeks)
- [ ] **Brand and category.** Pick 3 candidate brand names, run a trademark knock-out search (USPTO and EUIPO) plus domain checks, and write the "platform for one-person companies" copy.
- [ ] **Landing-page test, 2×2:** positioning ("One Person Company" vs "solo business") × kit (Consultant vs Property agent). Property agent is included only to size Phase 2 demand early. Measure waitlist conversion and pre-orders. Full experiment list: [marketing plan §4.5](./marketing-plan.md#45-first-six-experiments-ab-or-sequential).
- [ ] **30 interviews** across the Consultant, Coach, Creator, Designer and Property agent personas. Capture each person's *weekly recurring jobs* and their *approval threshold* (what they would let go out without looking).
- [ ] **Concierge pilot:** 15 paying users at $49–$79. The Paperclip engine runs behind the scenes with the outcome loop, and a human spot-checks the work.
- [ ] **Kill or pivot criteria:**
  - Fewer than 30% of pilot users retained at week 4.
  - First-pass acceptance of deliverables below 60%.
  - Cost per accepted deliverable above $1.50 on routine jobs.

### Phase 1: MVP (8–12 weeks)
- [ ] Onboarding interview that produces a business profile, then kit selection, then the first accepted deliverable in under 10 minutes.
- [ ] Four kits (Consultant, Coach, Creator, Creative freelancer) on three shared workflow engines. Each kit has 4–6 recurring workflows with outcome contracts.
- [ ] The outcome loop harness (checks, grader, approvals, trust ladder), a "Needs you" inbox, and a weekly results report.
- [ ] Flat pricing with dollar and job allowances; hard caps.
- [ ] Per-kit eval suites of 20–50 golden tasks, plus pass^3 consistency tracking.

### Phase 2: Category leadership
- [ ] *State of One-Person Companies 2027* report built on Census NES, pilot outcomes and surveys.
- [ ] Property agent kit with compliance guardrails; messaging channels; a kit marketplace for community creators.
- [ ] International pilots: India (OPC registration partners) and Korea (1인 기업 centers).

---

## Data Sources

**Primary data**
- US Census Bureau: [Nonemployer Statistics 2023 flat files](https://www2.census.gov/programs-surveys/nonemployer-statistics/datasets/2023/historical-datasets/); [NAICS code list](https://www2.census.gov/programs-surveys/nonemployer-statistics/technical-documentation/code-lists/); [receipts-size table NS2300NONEMP](https://data.census.gov/table/NONEMP2023.NS2300NONEMP); [2022 nonemployer story](https://www.census.gov/library/stories/2025/05/smallest-businesses.html); [Business Formation Statistics](https://www.census.gov/econ/bfs/index.html)
- Google Trends (pulled 2026-09-26 with pytrends): "one person company," "solopreneur," "one person business," "company of one," "AI agents," "AI employees," and industry "AI for X" terms
- RDAP domain registries (Verisign, Identity Digital, rdap.org), 2026-09-26
- [USPTO trademark search](https://tmsearch.uspto.gov/)
- Competitor pricing pages (rendered 2026-09-26): [Sintra](https://sintra.ai/pricing), [Marblism](https://www.marblism.com/pricing), [Lindy](https://www.lindy.ai/pricing), [NanoCorp](https://www.nanocorp.so/pricing), [PaperclipCloud](https://paperclipcloud.com/), [Paperclip.inc](https://paperclip.inc/), [Polsia](https://polsia.com/), [paperclip.ing](https://paperclip.ing/)
- [Anthropic API pricing](https://platform.claude.com/docs/en/about-claude/pricing); [Anthropic cost optimization guidance](https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence.md)

**Research and industry**
- [Carta Solo Founders Report](https://carta.com/data/solo-founders-report/); [Stripe Atlas 2025 review](https://stripe.com/blog/stripe-atlas-startups-in-2025-year-in-review); [MBO Partners 2025](https://www.mbopartners.com/state-of-independence); [Upwork Future Workforce Index 2026](https://investors.upwork.com/news-releases/news-release-details/upworks-future-workforce-index-2026-how-ai-redefining-value-work)
- [Korea 2025 one-person creative enterprise survey](https://www.korea.kr/briefing/pressReleaseView.do?newsId=156753709); [Venture Square](https://www.venturesquare.net/1074165/)
- [Rest of World on China OPC](https://restofworld.org/2026/china-ai-one-person-companies-incentives/); [Honghub 2026 OPC Insight Report](https://www.globenewswire.com/news-release/2026/04/29/3283960/0/en/Honghub-Unveils-2026-OPC-Insight-Report-Revealing-China-s-One-Person-Company-Boom-and-a-72x-AI-Labor-Advantage.html); [SCIO](http://english.scio.gov.cn/chinavoices/2026-04/02/content_118416270.html)
- [India MCA: One Person Company](https://www.mca.gov.in/content/mca/global/en/help-faq/faqs/company-services/incorporation/one-person-company.html)
- [ICF Global Coaching Study 2025](https://coachingfederation.org/blog/coaching-industry-continues-global-growth-with-5-34-billion-usd-revenue-new-research-reveals/); [NAR technology report 2026](https://www.nar.realtor/newsroom/realtors-adopt-technology-to-save-time-and-improve-the-client-experience-nar-report-finds); [Goldman Sachs creator economy](https://www.goldmansachs.com/insights/articles/the-creator-economy-could-approach-half-a-trillion-dollars-by-2027)
- [Gartner agentic AI cancellations](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027); [METR time horizons](https://metr.org/time-horizons/); [Sierra τ-bench](https://sierra.ai/blog/benchmarking-ai-agents); [Epoch AI](https://epoch.ai/data-insights/llm-inference-price-trends); [RevenueCat via TechCrunch](https://techcrunch.com/2026/03/10/ai-powered-apps-struggle-with-long-term-retention-new-report-shows)
- Small-business trust: [Small Business Expo](https://www.thesmallbusinessexpo.com/blog/the-trust-gap-small-businesses-are-using-ai-more-but-still-dont-fully-trust-it/); [KVIA/Stacker](https://kvia.com/stacker-small-business/2026/07/16/3-4-of-small-businesses-dont-trust-ai-for-basic-tasks/)

**Competitors and news**
- Polsia: [Trustpilot](https://www.trustpilot.com/review/polsia.com), [AIN](https://en.ain.ua/2026/05/25/ai-startup-polsia-with-no-employees-raised-30m-in-funding/), [Fortune](https://fortune.com/2026/03/26/the-one-person-unicorn-myth-miracle-future-of-startups-polsia/)
- NanoCorp: [preuve.ai analysis of NanoCorp updates](https://preuve.ai/blog/nanocorp-review), [Show HN](https://news.ycombinator.com/item?id=48062033)
- [Sintra seed round](https://tech.eu/2025/06/10/lithuanian-ai-startup-sintra-secures-17m-seed-empowering-smbs-with-ai-helpers/); [Motion Series C](https://www.usemotion.com/blog/motion-raises-60m-to-build-the-agentic-work-suite-for-businesses); [Taskade one-person companies](https://www.taskade.com/blog/one-person-companies)
- [Lofty and real estate AI](https://ascendix.com/blog/ai-real-estate-agents/); [coach AI clone pricing](https://personify.fyi/blog/ai-clone-cost/)
- [OpenAI small-business program](https://openai.com/index/introducing-chatgpt-small-business-program/); [Claude Cowork](https://techcrunch.com/2026/07/07/the-coding-agent-wars-are-spilling-into-the-rest-of-the-office-claude-cowork/)
- FTC: [Click Profit](https://www.ftc.gov/news-events/news/press-releases/2025/03/ftc-acts-stop-click-profit-online-business-opportunity-has-cost-consumers-least-14-million), [Operation AI Comply one year in](https://www.beneschlaw.com/insight/one-year-in-ftcs-operation-ai-comply-continues-under-new-administration-signaling-enduring-enforcement-focus/)
- [OPC Foundation terms](https://opcfoundation.org/terms-and-conditions/)

## Data Quality Notes

- **Census NES** counts *establishments* of businesses with no paid employees that file taxes. Side income shows up as small establishments, which is why 60.6% earn under $25K. The "≥$50K" filter is the best available proxy for "can pay."
- **Two similar figures, different meanings:** **7.46M** = *all* US nonemployers with ≥$50K receipts; **7.45M** = all nonemployers (any size) in the 13 target segments, of which **1.63M** earn ≥$50K.
- **Google Trends** values are relative indexes, not search volumes, and they carry sampling noise. Q3 2026 is a partial quarter.
- **The USPTO search** showed no results for the exact phrase. That is not legal advice; do a proper clearance search with counsel.
- **Domain checks**: `.ai` lookups for several exact names were rate-limited (HTTP 429), so their status is unknown.
- **Carta** figures come via secondary reporting because carta.com blocks automated access. **India OPC counts** vary by source (≈34K in Dec 2020; secondary sources cite ~86K active in 2025–26).
- **Competitor revenue** is self-reported (Polsia's figures range from $4.5M to ~$10M). **The unit-economics model** uses assumed workloads priced at list rates. Measure real usage in the concierge pilot.
