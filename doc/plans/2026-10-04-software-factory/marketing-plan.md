# Go-to-Market and Marketing Plan (v2): The AI Software Factory

**Date:** 2026-10-04 (replaces the [OPC marketing plan](../2026-09-26-opc-platform/marketing-plan.md))
**Part of:** [Market research v3](./market-research.md) · [Competitor analysis](./competitor-analysis.md) · [Factory lines](./factory-lines.md) · [Factory harness](./reliability-cost-harness.md) · [Product strategy v2](./product-feature-strategy.md) · [PRD v2](./prd.md) · [X build-in-public guide](./x-build-in-public-guide.md)
**Scope:**
- positioning, brand and landing page;
- developer channels and content;
- SEO and AI-search visibility;
- community, creators and partners;
- PR and the public benchmark;
- launch, gated paid acquisition, onboarding and lifecycle;
- measurement, budget, compliance, a 90-day calendar, expansion markets and launch copy.

**Working assumptions (from the approved decisions):**
- `[Brand]` is a placeholder until naming and trademark clearance ([market research §2.2](./market-research.md#22-naming-trademarks-and-domains)).
- **Audience:** solo technical founders, agencies and freelancers at beta; small teams at GA.
- **Pricing:** Solo $29 and Agency $399 platform fee per month (Team $199 at GA), plus **Small $3 / Medium $12 per merged change**; failed work free; bring-your-own-key option. 14-day trial with 10 free Medium changes.
- **Launch:** public beta in the **week of 25 January 2027 (W0)** with the Bug and Maintenance lines and a Feature-line preview. GA in late April 2027.
- **Message:** "engineers run the factory," not "replace engineers."
- The founder leads go-to-market with a DevRel/support lead from December and a few contractors.

---

## 0. Strategy on one page

| | |
|---|---|
| **Category** | **AI software factory.** Use it as a descriptive category; the brand is distinct ("Factory" belongs to Factory.ai; "Software Factory" is 8090's product name) |
| **Promise** | *"Specs in. Verified, shipped software out."* Audience line: *"Run a whole software company with a team of one."* |
| **Belief (founder voice)** | *"Engineers stop typing code and start running factories."* |
| **Enemy** | "Almost right" AI code, review overload, surprise bills, and agents that can delete production |
| **Beachhead ICP** | Solo technical founders and agencies/freelancers. About 220K core US accounts ([market research §3](./market-research.md#3-target-market)) |
| **Proof we sell** | Evidence card on every change · failed work is free · price before work · no production credentials for agents · a public weekly factory report, including failures · a public benchmark |
| **Primary channels** | ① Founder build-in-public on **X** and **YouTube** ("the factory builds the factory") ② **Hacker News** and **GitHub** (the open line format plus benchmark) ③ Developer newsletters and podcasts ④ SEO on jobs to be done ⑤ The Factory Floor community ⑥ Agency partnerships |
| **Later channels** | Paid search and newsletter sponsorships, *after* activation and CAC are proven; LinkedIn for CTOs and agency owners (GA) |
| **North Star** | **Weekly merged, verified changes per active account** |
| **12-month targets (base)** | 15K waitlist and email list · **1,500 paying accounts** (≈ $675K MRR at ≈ $450 blended revenue per account) · blended CAC ≤ $1,000 · monthly logo churn ≤ 4% |

---

## 1. Goals, KPIs and unit economics

### 1.1 Targets by phase (base case; conservative and stretch in brackets)

| Phase | Window | Targets |
|---|---|---|
| Foundations | W−16 → W−9 (October to November 2026) | Brand chosen and cleared · site v1 live · **2,000** waitlist · 12 design partners · 30 developer interviews · X following 1,500 |
| Partner alpha | W−8 → W−3 (December 2026) | 12 paying partners · first-pass merge rate ≥ 60% · 4 documented case studies · **4,000** waitlist · benchmark v0 (internal) |
| Pre-launch | W−2 → W−1 (January 2027) | **5,000** waitlist [2.5K / 9K] · 100 founding members (annual pre-pay) · 10 agency partners signed · 3 newsletter or podcast features booked |
| Launch month | W0 → W+4 | 1,000 trials [500 / 2,000] · **150 paying** [70 / 300] · activation ≥ 50% |
| Month 6 | W+24 | **600 paying** [300 / 1,200] · CAC ≤ $1,000 · churn ≤ 4% a month |
| Month 12 | W+48 | **1,500 paying** [700 / 3,500] · ≈ $675K MRR · GA lines L4 and L5 launched · second benchmark report |

**Sanity check against comparables:**
- Lovable reached $17M ARR three months after commercial launch ([Startup Riders](https://www.startupriders.com/p/how-lovable-hit-400m-arr-in-14-months)).
- Factory reported revenue doubling every month for six months in 2026 (press).
- Our base case is deliberately below these. We lead with trust and verification, not promotions, and we start with a narrow line set.

### 1.2 Unit economics that set channel limits

| Input | Assumption | Basis |
|---|---|---|
| Blended revenue per account | ≈ $450 a month. Mix: Solo 60% (≈ $200), Agency 25% (≈ $1,200), Team 15% from GA (≈ $900) | [Market research §6.3](./market-research.md#63-pricing-recommendation-decision-d5-to-validate-in-phase-0) |
| Gross margin | ≈ 55% | [Harness §6.3](./reliability-cost-harness.md#63-cost-per-change-assumptions-stated) |
| Monthly logo churn | 4% target | SMB SaaS benchmarks |
| Gross-profit lifetime value | $450 × 55% ÷ 4% ≈ **$6,200** | |
| **CAC ceiling** | LTV:CAC ≥ 3 → **≤ $2,000**; payback ≤ 8 months → **≤ $1,980** | Blended CAC target **≤ $1,000**; any single paid channel capped at $1,500 |
| Cost of a trial | 10 free Medium changes ≈ $50 cost plus failures ≈ **$60 per trial** | At 20% trial-to-paid, ≈ $300 per paying customer, counted in CAC |

**Worked example (Google search on job-to-be-done terms):**
1. CPC about $6 → visit-to-trial 5% → trial-to-paid 20%. That gives an ad CAC of **$600**.
2. Trial cost adds $300, for **≈ $900** in total. That is under target.
3. So paid works once landing-to-trial is ≥ 5% and trial-to-paid is ≥ 20%. Paid stays gated until both hold (§12).

---

## 2. Positioning and messaging

### 2.1 Positioning statement

> **For** solo founders, small software teams and development agencies
> **who** need to ship more than their headcount allows,
> **[Brand] is** the AI software factory
> **that** turns specs into verified, deployed and maintained software.
> **Unlike** coding agents that hand you code to check, or app builders that leave you with a prototype,
> **we** prove every change against its definition of done, keep agents away from production by design, and charge only for work that passes.

### 2.2 Messaging house

| Level | Message | Proof points |
|---|---|---|
| **Umbrella** | Specs in. Verified, shipped software out. | Lines, the evidence card, the weekly factory report |
| **Pillar 1: Proof, not promises** | Every change carries evidence: tests written first, hidden scenarios, scans, a preview. | Evidence card; published first-pass merge and false-green rates per line; public benchmark |
| **Pillar 2: Safe by construction** | Agents can't touch production. Not "shouldn't": can't. | No production credentials in sandboxes; separate merge identity; High tier always human; Safety page |
| **Pillar 3: Decide, don't review** | Approve on evidence in seconds. Earn lights-out for boring work. | Evidence inbox, batch approval, lights-out ladder with track records |
| **Pillar 4: Pay for outcomes** | A price before work starts. Charged only on merge. Failed work is free. | Small $3 / Medium $12; caps; bring-your-own key; false-green refunds |
| **Pillar 5: Any model, your code** | The best agent for each job, and your repository stays yours. | 12 agent adapters; normal Git and CI; export everything |

### 2.3 Language rules (brand, legal and trust)

| ✅ Say | ❌ Never say | Why |
|---|---|---|
| "verified change," "evidence," "merged," "factory," "line," "lights-out" (once earned) | "replace your engineers," "no engineers needed," "fire your team" | Our champions are engineers; hiring data doesn't support it; FTC substantiation |
| "first-pass merge rate of X% on [line] in [period]" (measured, with the method linked) | "bug-free," "100% accurate," "guaranteed," "10x" without data | FTC substantiation; the honesty brand |
| "AI-generated, verified by checks, approved by you" | Implying a human wrote factory output | Transparency; PRs are labeled "Generated by [Brand]" |
| "can't access production" (only while true in the product) | "secure" or "unhackable" without qualification | Security claims must be precise |
| Comparisons that state competitors' strengths fairly | Disparaging competitors | Credibility with engineers; legal risk |

**Founder exception.** In your personal build-in-public voice, you may say you *believe* software will be made by factories run by a few engineers. Frame it as a belief and a bet, never as a product claim.

### 2.4 Competitive one-liners (fair, for comparison pages and replies)

| Alternative | Line |
|---|---|
| Coding agents (Claude Code, Codex, Cursor) | "Keep your favorite agent; [Brand] runs it as a factory, with tests first, hidden scenarios, a separate merge identity and a price per merged change." |
| Autonomous engineers (Devin) | "Same ambition, different deal: self-serve, a price before each change, failed work free, and a refund if it breaks main within 7 days. No annual contract needed." |
| **Factory** (factory.com) | "Factory gives you the parts to build a software factory. We run one for you, and you pay only for changes that merge." State their strengths fairly: excellent harness, broad coverage, air-gapped enterprise options |
| **Warp Factories** | "Warp gives you the infrastructure to build and tune your own factory. We run one for you, safe by default, and you pay only for changes that merge." State their strengths fairly: open to any model or harness, factories as code, strong measurement and self-improvement |
| 8090 | "Built for teams of 1–20, self-serve, live in 30 minutes." |
| App builders (Lovable, Replit, Bolt) | "For engineers who need production-grade, maintained software, not a prototype." |
| Hiring a contractor | "A Medium change costs $12 and comes with evidence. Keep your contractor for the hard problems." (Compare against a real rate.) |

### 2.5 Value propositions by persona

| Persona | Headline | Top 3 things to feature |
|---|---|---|
| **Sam, solo founder** | "Your SaaS, maintained while you sleep." | Bugs fixed with proof · dependencies and advisories handled · features from a spec |
| **Ines, agency owner** | "Your studio, multiplied." | Client workspaces · per-client cost reports · handover packs |
| **Dana, freelancer** | "Finish fixed-price work faster, with receipts." | Evidence cards for clients · predictable cost · Greenfield blueprint |
| **Raj, CTO** (GA) | "Ship more without hiring, and without breaking main." | DORA metrics · risk tiers · review routing |

---

## 3. Brand foundations

- **Naming:**
  - **Category crowding:** Factory's headline is "Build your software factory", Warp sells "cloud software factories", Tessl uses similar wording, and 8090 has a USPTO application for "8090 SOFTWARE FACTORY". Use "AI software factory" only descriptively, and get counsel before using it in a product name or headline. Pending decision C5 in the [competitor analysis](./competitor-analysis.md#8-what-this-changes-in-our-plan-recommendations): lead with "verified software factory" or "verified changes."
  - Use a coined name, or a short word plus a `.dev` or `.ai` domain and a `get…` or `use…` `.com`. Every compound `.com` we checked was taken; `.dev` versions such as linewright.dev, provenline.dev and factoryofone.dev were free on 2026-10-04 ([market research §2.2](./market-research.md#22-naming-trademarks-and-domains)).
  - Run USPTO and EUIPO knock-out searches in classes 9 and 42 for 3 finalists.
  - Secure handles on X, GitHub, YouTube, Bluesky, LinkedIn, Reddit and Discord.
- **Category assets:**
  - **The evidence card** is the hero visual everywhere.
  - **"Lights-out" badges** per line (for example "Maintenance: lights-out since March") that customers can show in their README. This is a share loop.
  - **A published definition** we repeat: *"An AI software factory turns specs into verified, released and maintained software, with evidence for every change and humans deciding only where risk requires it."*
- **Voice:** precise, calm, technical, honest. Show numbers and failures. No hype words. No robot imagery.
- **Visual system:** dark-and-light terminal-native look; the evidence card and the factory floor board; real screenshots only.

---

## 4. Landing page

### 4.1 Objectives and stack
- **Pre-launch goal:** waitlist sign-up with segmentation (role, stack, team size, repositories). **Launch goal:** connect a repository (trial start).
- **Stack:**
  - a fast static site (under 1.5 seconds on mobile);
  - PostHog for product analytics and flags;
  - UTMs, consent banner, WCAG 2.2 AA;
  - server-side sign-up events.
- **Benchmarks:** SaaS landing pages convert at a **3.8% median** ([LanderLab](https://landerlab.io/blog/landing-page-conversion-rate)).
- **Targets:** waitlist 10–20% from warm X and Hacker News traffic; landing-to-trial ≥ 5% at launch.

### 4.2 Page architecture with draft copy

| # | Section | Draft copy and content | Purpose |
|---|---|---|---|
| 1 | **Hero** | **H1 (A):** "Specs in. Verified, shipped software out." **H1 (B):** "Run a whole software company with a team of one." Sub: "[Brand] is an AI software factory. It fixes bugs, keeps dependencies current and builds features, and proves every change before you merge it." CTA: **"Join the beta"** (pre-launch) / **"Connect a repo — first change free"** (launch). Visual: a 15-second loop of an order going from issue to evidence card | Clarity in 5 seconds |
| 2 | **The evidence card** | A real card: ✓ reproduced before the fix · ✓ 412 tests pass · ✓ no new security findings · ✓ reviewed · preview link · cost $4.10 · price $12 | The differentiator |
| 3 | **Problem** | "Agents write code fast. You still review it, test it, secure it, pay for its mistakes, and hope it never touches prod." Three cards: review overload · surprise bills · production risk | Empathy |
| 4 | **How it works** | ① Connect a repo (Repo X-ray, read-only) ② Approve suggested orders ③ The factory plans, builds and verifies in sandboxes ④ Approve on evidence, or let boring work go lights-out ⑤ Friday: the factory report | The mechanism |
| 5 | **Lines** | Bug · Maintenance · Feature (preview) · Greenfield and Agency (coming at GA), each with "what done means" | Depth |
| 6 | **Safety** | "Agents can't touch production." A capability table (what agents can and can't do), linked to the Safety page | Remove the biggest fear |
| 7 | **Pricing** | "$3 small, $12 medium. Charged only when merged. Failed work is free. Set a hard monthly cap." Plan table; bring-your-own-key option | Remove price anxiety |
| 8 | **Proof** | Design-partner case studies (real, permissioned); published line metrics; benchmark link | Credibility |
| 9 | **Any model** | Logos of supported agents and models (with permission or as plain text) | Neutrality |
| 10 | **FAQ** | "Does it ever push to main without me?" · "What happens when it fails?" · "Can it see my secrets?" · "Which models?" · "Do you train on my code?" (No.) · "Can I leave and keep everything?" (Yes.) | Objections |
| 11 | **Final CTA and footer** | Repeat the CTA; AI-use notice; privacy; terms; "What is an AI software factory?" | Close |

### 4.3 Line and audience pages

- **Line pages:** `/lines/bug`, `/lines/maintenance`, `/lines/feature`, then `/lines/greenfield` and `/lines/agency` at GA. Each has:
  - what done means;
  - an example evidence card;
  - a live metric (first-pass merge rate, last 30 days, once measured);
  - FAQs.
- **Audience pages:** `/for/founders`, `/for/agencies`, `/for/freelancers`, and `/for/teams` at GA.
- These pages double as SEO pages ("automatically fix bugs from Sentry," "automate dependency upgrades with tests") and as ad destinations.

### 4.4 Waitlist mechanics

- **Form:** email, GitHub username, role, stack, team size, and "the first thing you'd hand the factory."
- **Referral queue:** move up the list by inviting others. Rewards are early access and the founding-member price.
- **Founding members (first 500):** 40% off the platform fee for year one, a "Founding Factory" badge, and a vote on the line roadmap. **No lifetime deals:** inference costs are open-ended.
- **Nurture:** the weekly Factory Report email; early benchmark results; office-hours invites.

### 4.5 First six experiments

| # | Test | Hypothesis | Metric |
|---|---|---|---|
| 1 | "Specs in, software out" vs "Software company of one" hero | The outcome promise beats the identity promise for engineers | Waitlist conversion |
| 2 | Evidence card above the fold vs the factory-floor animation | Concrete proof beats motion | Conversion, scroll depth |
| 3 | Price shown vs "pricing at launch" | Transparent outcome pricing filters for real buyers | Pre-pay rate |
| 4 | "First change free" vs "10 free changes" framing | Single-step framing lifts repository connects | Trial start |
| 5 | Safety section high vs low on the page | Production fear is a top objection for founders | Conversion by persona |
| 6 | Line page vs home page as the ad destination | Specific beats generic | Cost per trial |

### 4.6 Landing-page compliance checklist
- [ ] No unproven productivity or replacement claims. Every number is measured, dated and linked to its method (FTC substantiation).
- [ ] Testimonials are real, attributed and permissioned. No fake or AI-written reviews. The FTC rule allows penalties up to **$51,744 per violation** ([FTC](https://www.ftc.gov/news-events/news/press-releases/2024/08/federal-trade-commission-announces-final-rule-banning-fake-reviews-testimonials)).
- [ ] Safety claims match the product exactly. Re-check at every release.
- [ ] Competitor names are used only factually; logos only with permission.
- [ ] Cookie consent; CAN-SPAM-compliant email; WCAG 2.2 AA.

---

## 5. Audience and channel strategy

### 5.1 Where the audience spends time

| Platform | Signal | Best for | Notes |
|---|---|---|---|
| **GitHub** | Used by 67% of developers as a community platform ([Stack Overflow 2025](https://survey.stackoverflow.co/2025/)); 180M+ developers on the platform | Open line format, benchmark, examples; the product itself (PRs and checks) | Our PR labels and evidence summaries are seen by every reviewer: organic distribution |
| **YouTube** | 61% of developers use it as a community platform (Stack Overflow 2025) | Long-form "factory floor" demos and teardowns | Real repositories, real failures |
| **Hacker News** | Only about 2.3% of submissions reached the front page in Q1 2026; the median Show HN scored 2 points, and 50 points is the top 6% ([daily.dev](https://business.daily.dev/resources/hacker-news-marketing-developer-tools-show-hn-launch-day-sustained-coverage/)) | Technical launches (holdout scenarios, false-green audits, the benchmark) | Skeptical, high-intent; no marketing tone; answer every question |
| **X** | The center of AI-engineering and indie-hacker conversation | Build in public; founder voice; launch spikes | See the [X guide](./x-build-in-public-guide.md) |
| **Reddit** | Strongly cited in AI answers ([ZipTie](https://ziptie.dev/blog/why-reddit-dominates-chatgpt-perplexity-and-google-ai-overviews/)) | r/SaaS, r/webdev, r/ExperiencedDevs, r/devops, r/indiehackers | Participate as a person; follow each subreddit's rules |
| **Newsletters and podcasts** | AI-engineering, web-dev and indie-founder newsletters and podcasts | Sponsorships and guest spots after launch | Track cost per trial per issue |
| **Discord** | Where developer communities gather | The Factory Floor community | — |
| **LinkedIn** | CTOs and agency owners | GA (Team plan, Agency line) | Document posts; links in comments |

### 5.2 Channel priorities

| Tier | Channels | Why |
|---|---|---|
| **1: Build now** | Founder X + YouTube · GitHub (open line format, benchmark harness) · Factory Report newsletter · line and audience pages for SEO | Low CAC, compounding, credible with engineers |
| **2: Add at partner alpha** | Factory Floor Discord · Reddit participation · agency partner program · developer creator collaborations | Social proof and reach into agencies |
| **3: Launch and scale** | Show HN · Product Hunt · launch week · newsletter and podcast sponsorships · paid search (gated) · LinkedIn (GA) | Spikes, then scale once conversion is proven |

---

## 6. Content strategy

### 6.1 The big idea: "The factory builds the factory"

[Brand] is built **by [Brand]**. Every Friday the founder publishes the product's own **Factory Report** for the [Brand] repository:
- orders merged, by line;
- first-pass merge rate;
- false-green audit;
- cost per change;
- lights-out share;
- **what failed and why.**

**Why it works:**
- It demonstrates the product and the honesty positioning in one artifact.
- It gives a weekly rhythm.
- It's a story engineers want to check for themselves.

**Rules:**
- Real numbers only.
- Show failures.
- Never post customer code or secrets.
- Disclose what was AI-generated.

### 6.2 Content pillars

| Pillar | Share | Examples |
|---|---|---|
| **Factory floor** (proof) | 35% | The weekly Factory Report · "watch a bug go from issue to verified PR in 11 minutes" · a lights-out promotion with its evidence |
| **How we verify** (engineering) | 25% | Holdout scenarios vs test gaming · why build agents can't merge · the false-green audit · order sizing from METR horizons |
| **Data and research** | 15% | Benchmark results · cost per verified change by model · "State of AI Software Factories" |
| **Playbooks** | 15% | "Make your repo factory-ready in an afternoon" · "a maintenance policy you can automate" · agency handover packs |
| **Founder journey** | 10% | Decisions, mistakes, pricing experiments, the pivot story |

### 6.3 Cadence and formats (founder plus 1 editor)

| Platform | Weekly cadence | Formats |
|---|---|---|
| X | Daily posts; 1 thread a week; replies daily | Factory Report, build logs, research threads (see the X guide) |
| YouTube | 1 long-form (8–15 min) + 2 Shorts | Factory-floor demos, teardowns, benchmark readouts |
| GitHub | Weekly releases of the line format and benchmark harness; examples | Open source |
| Newsletter | 1 a week: "The Factory Report" | Report, one engineering deep dive, one community line |
| Blog / SEO | 2 articles a week before launch, then 3 | §7 |
| Reddit / Hacker News | 2–3 helpful contributions a week; launches only when there's something technical to show | Answers, data |
| LinkedIn (GA) | 2 posts a week | Agency and CTO angles |

### 6.4 Hooks and templates (draft; numbers are placeholders until measured)

- **X:** "Week 9 of building [Brand] with [Brand]. 63 changes merged. First-pass merge 71%. 1 false green (here's the postmortem). Cost per change: $4.80. Lights-out: dependency patches only ↓"
- **X thread:** "Our agents kept 'fixing' tests instead of code. Here's how hidden holdout scenarios stopped it (and what METR found about reward hacking)."
- **YouTube title:** "I let an AI software factory maintain my SaaS for 30 days (the honest results)."
- **Show HN:** "Show HN: Holdout scenarios, a way to verify AI code changes without reading every line."
- **Reddit (value first, r/SaaS style):** "We measured cost per *merged* AI change across 5 models on real repos. Here's the data and the method."

### 6.5 AI-generated creative and code-sharing policy
- No synthetic human presenters or testimonials.
- Label AI-generated visuals; follow platform AI-disclosure rules.
- **Never show customer code, repository names or secrets** without written permission. Blur by default.
- Report security issues in third-party projects privately first (responsible disclosure), never as content.

---

## 7. SEO and AI-search visibility

| Cluster | Target queries | Asset |
|---|---|---|
| **Category** | "AI software factory," "software factory AI," "dark factory software," "levels of AI coding" | A canonical guide ("What is an AI software factory?") plus a glossary (Shapiro's levels, holdout scenarios, false green) |
| **Jobs to be done** | "automatically fix bugs from Sentry," "automate dependency upgrades," "AI code review with tests," "fix flaky tests automatically," "keep dependencies up to date automatically" | Line pages with example evidence cards |
| **Problems** | "AI code review takes too long," "AI generated code security," "Claude Code cost per developer," "AI agent deleted database" | Honest explainers with data and our approach |
| **Comparisons** | "Devin alternative," "Factory AI alternative," "Copilot coding agent vs …" | Fair comparison pages that state strengths |
| **Data** | "cost per AI code change," "AI coding agent benchmark real repos" | The public factory benchmark and the State of AI Software Factories report |

**AI-search visibility:**
- AI answers cite Reddit, YouTube, Wikipedia and GitHub heavily ([Semrush](https://www.semrush.com/blog/most-cited-domains-ai/)). Being present and genuinely useful on those platforms *is* the strategy.
- Publish quotable definitions and benchmark numbers with dates.
- Keep company facts consistent across sites.
- Test brand prompts monthly in ChatGPT, Claude, Gemini and Perplexity.

---

## 8. Community: the Factory Floor

- **Why:** engineers trust peers and evidence. A community around the **open line format** and the **benchmark** creates both.
- **Format:**
  - A Discord, open to non-customers, with channels per stack and per line.
  - **"Lights-out Friday,"** a weekly live stream: members show a line that earned lights-out, with its evidence.
  - Monthly **community line reviews:** proposed lines must publish evals and pass^3.
  - A quarterly **Factory Sprint:** a public challenge to make an open-source repository factory-ready.
- **Share loops:**
  - "Lights-out" README badges;
  - the shareable weekly report card;
  - PRs labeled "Generated by [Brand]" with an evidence summary, seen by every reviewer.
- **Rules:**
  - no hype or "replace engineers" posts;
  - real results only;
  - security issues reported privately.
- **KPIs:**
  - weekly active members;
  - community line submissions;
  - trials from the community;
  - benchmark contributions.

---

## 9. Creators, affiliates and partners

### 9.1 Developer creators
- **Who:** 10–20 developer YouTubers and streamers (20K–300K subscribers) who build real products on camera, plus AI-engineering writers.
- **Deal:** a flat fee plus affiliate commission. The brief is **an unscripted week of the factory on their own repository, failures included**. The creator has full editorial control and must disclose the paid partnership.
- **Tracking:** unique links and codes. Renew only creators under the $1,500 per-paying-account cap.

### 9.2 Affiliate program
- **Terms:** 20% recurring for 12 months on platform fees and change charges.
- **Guardrails:**
  - mandatory disclosure;
  - an approved-claims library;
  - no bidding on our brand;
  - affiliates who make "replace engineers" or unmeasured claims are removed.

### 9.3 Strategic partners (by phase)

| Partner type | Value exchange | Phase |
|---|---|---|
| **Development agencies** (10 at beta) | Agency plan discount and co-marketing case studies; they become our most credible references | Beta |
| **Paperclip open-source community** | Contribute general improvements upstream; publish the line format as teams-catalog packages; credibility and goodwill | Beta |
| Sandbox providers (E2B, Daytona, Modal) | Co-marketing (case study, template); capacity credits | Beta |
| Deploy platforms (Vercel, Railway, Fly) | Integration listings; preview-environment templates | Beta → GA |
| Error tracking (Sentry) | Integration listing; "from error to verified fix" joint content | GA |
| Startup programs (accelerators, founder communities) | Credits for portfolio companies | GA |

---

## 10. PR and category creation

- **Anchor assets:**
  1. **The public factory benchmark** (launch week). It reports cost per verified change, first-pass merge rate and false-green rate by model and agent, on real repositories with hidden holdout scenarios.
  2. **The State of AI Software Factories 2027** report (GA). It combines benchmark data, design-partner outcomes, survey data and market data ([market research](./market-research.md)).
- **Story angles:**
  1. **Contrarian:** "AI won't replace engineers this year. Here's the work it can already do without them, with proof." (Data from lights-out lines.)
  2. **Founder story:** a software company built by its own factory, in public.
  3. **Honesty:** "The AI coding tool that refunds you when it's wrong" (false-green refunds).
  4. **Safety:** "Why our agents can't delete your database" (a PocketOS-style failure, prevented by design).
- **Targets:**
  - tech press;
  - AI-engineering newsletters and podcasts;
  - developer YouTube;
  - founder communities.
- **Mechanics:** embargoed benchmark briefings 2 weeks before launch; a reproducible method on GitHub; the founder available for podcasts.
- **Reviews:** invite real users to G2 and Trustpilot, with no incentives tied to positive ratings.

---

## 11. Launch plan

### 11.1 Timeline (W0 = launch week; week of 25 January 2027)

| Weeks | Dates (target) | Workstream highlights |
|---|---|---|
| W−16 → W−13 | October 2026 | Naming and trademark knock-out · handles and domains · site v1 with waitlist · Phase 0 partners recruited (12) · founder X and YouTube cadence starts · 30 interviews |
| W−12 → W−9 | November 2026 | Landing tests 1–3 · first public Factory Report (of the [Brand] repository) · benchmark design published on GitHub · agency partner terms · Phase 0 readout |
| W−8 → W−5 | December 2026 | Partner alpha · case studies (permissioned) · creator outreach · Factory Floor Discord opens · line pages live |
| W−4 → W−1 | January 2027 | Private-beta cohorts from the waitlist · founding-member offer · Product Hunt "upcoming" page · embargoed benchmark briefings · 60–90-second demo · load and cost caps tested |
| **W0** | **25–29 January 2027** | **Launch week** (below) |
| W+1 → W+4 | February 2027 | Onboarding and conversion optimization · gated paid tests if conditions are met (§12) · first Lights-out Friday stream |
| W+5 → W+12 | March–April 2027 | Scale what works · Team plan and GitLab · **GA launch (late April)**: Feature line GA, Greenfield and Agency lines, State of AI Software Factories report |

### 11.2 Launch week, one announcement a day

| Day | Announcement | Channels |
|---|---|---|
| **Tue** | **Public beta launch:** Bug and Maintenance lines; Feature-line preview; founding pricing | Founder X thread and video · newsletter · Product Hunt · Discord live |
| **Wed** | **Show HN:** "Holdout scenarios: verifying AI code changes without reading every line" (technical post plus open-source runner) | Hacker News · GitHub · X thread |
| **Thu** | **Public factory benchmark v1** (cost per verified change by model and agent) | Embargo lifts with newsletters and podcasts · GitHub · Reddit data post where allowed |
| **Fri** | **First public weekly Factory Report** for the [Brand] repository, including failures | X · YouTube long-form · blog |
| **Sat–Sun** | **Lights-out Friday special (live):** watch the maintenance line run on a real open-source repository; founding offer closes Sunday | YouTube Live · Discord · email |

**Expectations:**
- **Product Hunt:** a top-3 finish brings about 5K–15K visitors, with about 10–30 sign-ups per 1,000 visitors ([shno.co](https://www.shno.co/marketing-statistics/product-hunt-launch-statistics)). Treat it as awareness.
- **Show HN:** high-intent and skeptical. Plan for no front page, and prepare for it anyway.
- **The waitlist is the main source of trials.**

### 11.3 Launch-day checklist
- [ ] Status page, error alerts and cost dashboards live; trial caps on; sandbox capacity reserved; on-call rota.
- [ ] Onboarding tested end to end on 20 public repositories (first merged change ≤ 30 minutes).
- [ ] The Safety page matches the shipped product (security review sign-off).
- [ ] Support macros, docs and a "known issues" page.
- [ ] UTMs on every link; creator codes ready.
- [ ] A rapid-response plan for criticism: answer publicly and specifically; fix or explain within 24 hours.

---

## 12. Paid acquisition (gated tests)

**Only start paid when all three hold:**
- landing-to-trial ≥ 5%;
- activation (first merged change) ≥ 50%;
- trial-to-paid ≥ 20%.

Run the first tests at **$15K in total** over 4–6 weeks.

| Channel | Test design | Kill or scale rule |
|---|---|---|
| **Google Search** | Job-to-be-done terms ("automate dependency upgrades," "fix bugs from Sentry automatically"), category terms, fair competitor comparisons | Kill if CAC > $1,500 after $3K; scale while ≤ $1,000 |
| **Newsletter and podcast sponsorships** | AI-engineering and indie-founder newsletters; one issue each, with a unique code | Renew if cost per paying account ≤ $1,000 |
| **YouTube** (in-feed) | Promote the best organic factory-floor demo | Same |
| **Reddit ads** | r/SaaS, r/webdev, r/devops with transparent offers | Same |
| **LinkedIn** (GA) | Boost founder posts to CTOs and agency owners | Keep only if trial-to-paid is exceptional |

**Creative principles:**
- Show the evidence card in the first 3 seconds.
- Real repositories (with permission) and real numbers.
- No synthetic people.
- Every claim substantiated.

---

## 13. Conversion, onboarding and lifecycle

### 13.1 Trial design
- **Terms:** 14 days, **no card**, **10 free Medium changes**. Trial cost is capped at about $60.
- **Activation:**
  - the first merged, verified change within 30 minutes of connecting;
  - **3 merged changes in week 1.**
- **Card-required test:** after W+4, once onboarding quality is proven. Benchmarks: no-card trials convert at a median of about 14%; card-required about 44%, with 30–50% less volume ([shno.co](https://www.shno.co/marketing-statistics/free-trial-conversion-statistics)).

### 13.2 Onboarding sequence (in-app plus email)

| Day | Trigger | Message / action |
|---|---|---|
| 0 | Sign-up | GitHub App install → Repo X-ray → five suggested orders → approve one → watch it run |
| 0 | First merge | 🎉 "Your first verified change." Show the evidence card and what each check proved |
| 1 | No second order | "Your X-ray found 9 vulnerable dependencies. Patch them for $3 each, charged only if merged." |
| 3 | Maintenance not enabled | "Turn on the Maintenance line: weekly patches, flaky tests, docs. You approve everything until it earns lights-out." |
| 5 | First Friday | **Weekly Factory Report:** the "aha" email |
| 7 | Mid-trial | Invite to Lights-out Friday; a tip for making the repository factory-ready |
| 10 | Pre-decision | "What your factory did so far," plus a plan recommendation from actual usage and a cap suggestion |
| 13 | Last day | Honest summary; founding price if eligible; export option |

### 13.3 Retention and virality
- **The weekly Factory Report** is the retention engine and the share unit (a redacted share card).
- **PR labels and evidence summaries** reach every reviewer and collaborator.
- **Lights-out README badges.**
- **Referral:** double-sided, one free month of platform fee each, offered after a positive moment (a lights-out promotion, a strong weekly report).
- **Win-back:** 30 days after churn, send what changed (new lines, measured first-pass merge improvements).

---

## 14. Measurement

| Stage | Metric | Target |
|---|---|---|
| Awareness | Share of voice for "AI software factory"; benchmark citations; brand-prompt answers in AI assistants | Top 3 for "AI software factory" by month 6 |
| Acquisition | Waitlist conversion · repository connects · cost per trial by channel | §4, §12 |
| Activation | First merged change ≤ 30 minutes; 3 merged in week 1 | ≥ 50% |
| Revenue | Trial-to-paid · revenue per account · payback | ≥ 20% (no card) · ≈ $450 · ≤ 8 months |
| Retention | Monthly logo churn; weeks with ≥ 1 merged change | ≤ 4% |
| Trust | Published first-pass merge and false-green rates per line; support first response | False green = 0; ≤ 1 business hour |
| Referral | Share of new accounts from referrals and PR exposure | 20% |
| **North Star** | **Weekly merged, verified changes per active account** | Rising every month |

**Attribution:** UTMs; "How did you hear about us?"; creator codes; PostHog funnels; monthly cohort review by channel, persona and line.
**Weekly ritual (30 minutes):** funnel, best and worst content, the CAC table, one experiment decision.

---

## 15. Compliance and risk (marketing)

| Risk | Rule / control |
|---|---|
| Productivity and replacement claims | Only measured, dated claims with a published method; no "replace engineers" in product marketing |
| Fake or incentivized reviews | FTC rule: no fake, AI-written or undisclosed insider reviews; penalties up to $51,744 per violation |
| Endorsements | Creators and affiliates disclose; we keep records |
| Security claims | Precise, reviewed by security before each release; no "unhackable" |
| Customer code in content | Never without written permission; blur by default |
| Open-source etiquette | Contribute fixes upstream; respect licenses; no spam PRs to open-source repositories for marketing |
| Platform rules | Hacker News and Reddit self-promotion rules; no vote rings, bots or fake accounts |
| Category hype backlash | Publish failures; answer criticism with data |

---

## 16. Budget (first 6 months, excluding salaries)

| Line | Lean ($30K) | **Base ($90K)** | Growth ($220K) |
|---|---|---|---|
| Newsletter, podcast and creator sponsorships | $8K | $30K | $70K |
| Paid tests → scale (gated) | $5K | $25K | $100K |
| Benchmark compute and State report | $5K | $10K | $15K |
| Content and video production | $5K | $12K | $20K |
| Community, events, launch | $3K | $5K | $7K |
| Tools (site, analytics, email) | $2K | $3K | $3K |
| Contingency | $2K | $5K | $5K |

**Team:**
- Founder: voice, content, community.
- DevRel/support lead from December.
- Part-time video editor.
- Fractional PR for launch month.
- Partner manager (part-time) for agencies from W−8.
- The factory itself builds the product and produces the weekly report (dogfooding).

---

## 17. 90-day calendar (W−12 → W0), weekly

| Week | Key deliverables |
|---|---|
| W−12 | Brand chosen and cleared; site v1 plus waitlist live; analytics; partner recruiting |
| W−11 | Founder cadence live (X daily, YouTube weekly); newsletter #1 |
| W−10 | Landing test 1; first public Factory Report; benchmark method on GitHub |
| W−9 | Landing test 2; Phase 0 readout; agency partner terms |
| W−8 | Partner alpha starts; line pages live; Discord opens |
| W−7 | First case study; creator outreach wave 1 |
| W−6 | Landing test 3; press and newsletter list; Show HN draft |
| W−5 | Case studies 2–3; creators signed (10); demo script |
| W−4 | Private-beta cohort 1 (founders); Product Hunt upcoming page |
| W−3 | Cohort 2 (agencies); benchmark v1 runs; embargo briefings |
| W−2 | Cohort 3; founding offer opens; launch assets finished |
| W−1 | Launch rehearsal; load and cost caps; creator content scheduled |
| **W0** | **Launch week** (§11.2) |

---

## 18. Expansion markets (after US product–market fit)

| Market | Why | Channels | Notes |
|---|---|---|---|
| **India** | Large professional developer and agency base; strong English-language developer communities | X, YouTube, LinkedIn; agency partnerships | INR pricing; agency line first |
| **UK / EU** | Many small software firms; customers' EU Cyber Resilience Act duties make evidence and SBOMs valuable | LinkedIn, X, meetups | GDPR-first data story; EU data residency (P2) |
| **Latin America** | Fast-growing nearshore agency market serving US clients | LinkedIn, YouTube, communities | Agency line; per-client reporting |

---

## Appendix A: Launch copy (drafts)

- **Product Hunt tagline (≤ 60 characters):** "An AI software factory that proves every change."
- **Product Hunt first comment (outline):**
  1. Who the founder is, and that the product builds itself.
  2. The problem: fast code, slow trust; surprise bills; production risk.
  3. What's different: evidence cards, hidden scenarios, a separate merge identity, a price per merged change, failed work free.
  4. Lines available today.
  5. Honest limits.
  6. The ask: which line to build next.
- **Show HN title:** "Show HN: Holdout scenarios, verifying AI code changes without reading every line"
- **Launch email subjects:** "Your factory is ready" · "First verified change on us" · "We're live: bugs and maintenance, with proof"
- **Founder X launch thread (outline):**
  1. The belief.
  2. What the factory did on our own repository last week (real numbers).
  3. One failure and the fix.
  4. The evidence card.
  5. Pricing.
  6. Link in the last post.

---

## Sources

- Developer channels: [Stack Overflow 2025 survey](https://survey.stackoverflow.co/2025/) · [daily.dev on Hacker News launches](https://business.daily.dev/resources/hacker-news-marketing-developer-tools-show-hn-launch-day-sustained-coverage/) · [Product Hunt statistics](https://www.shno.co/marketing-statistics/product-hunt-launch-statistics) · [ZipTie: Reddit in AI answers](https://ziptie.dev/blog/why-reddit-dominates-chatgpt-perplexity-and-google-ai-overviews/) · [Semrush most-cited domains](https://www.semrush.com/blog/most-cited-domains-ai/)
- Conversion: [LanderLab landing benchmarks](https://landerlab.io/blog/landing-page-conversion-rate) · [Free-trial conversion](https://www.shno.co/marketing-statistics/free-trial-conversion-statistics)
- Growth comparables: [Startup Riders: Lovable](https://www.startupriders.com/p/how-lovable-hit-400m-arr-in-14-months) · [DevOps.com: Factory](https://devops.com/factory-raises-200m-as-it-builds-agents-across-the-software-lifecycle/)
- Compliance: [FTC reviews rule](https://www.ftc.gov/news-events/news/press-releases/2024/08/federal-trade-commission-announces-final-rule-banning-fake-reviews-testimonials)
- Market and product evidence: see the [market research v3](./market-research.md#data-sources) and the [harness](./reliability-cost-harness.md#sources).

**Data notes:** channel and conversion benchmarks are mostly secondary sources and vary widely. Replace them with our own measured numbers within 4–6 weeks of each test.
