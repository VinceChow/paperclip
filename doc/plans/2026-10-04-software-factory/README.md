# AI Software Factory: Plan Set

Date: 2026-10-04

This folder holds the research and plans for [Brand], an **AI software factory for small software companies**: solo technical founders, teams of up to 20 engineers, and development agencies and freelancers. Specs go in; planned, built, tested, secured, deployed and maintained software comes out, with evidence for every change.

It replaces the [one-person-company (OPC) platform plan set](../2026-09-26-opc-platform/README.md), which is kept unchanged for history.

## Decisions in force (approved 2026-10-04)

| # | Decision |
|---|---|
| D1 | Target small software companies first: solo technical founders, teams ≤ 20, agencies and freelancers. Expand to mid-market later |
| D2 | Message: "Engineers run the factory." "Replace engineers" is the founder's belief, not a product claim |
| D3 | "One Person Company" is used only as an audience phrase ("one-person software company") |
| D4 | Build on a fork of Paperclip for the control plane |
| D5 | Outcome pricing: a small platform fee plus a price per merged change (Small $3, Medium $12), failed work free; bring-your-own-key option |
| D6 | Launch at autonomy Level 4; lights-out is earned per line from measured track records |
| D7 | Public beta in the week of 25 January 2027 (Bug + Maintenance lines, Feature-line preview); GA in late April 2027 |
| D8 | New dated folder; OPC documents kept with "superseded" banners |
| D9 | Front office, revenue loop, content engine and property kit are parked (a possible later "OPC operations" layer) |

## Documents

0. [**pivot-proposal.md**](./pivot-proposal.md): the approved proposal that moved from the OPC platform to the software factory. It covers the evidence, the options, the per-document change list and the nine decisions.
1. [**market-research.md**](./market-research.md) (v3): market and money, adoption, the METR capability trend, the verification and cost bottleneck, and sizing (about 220K core US accounts). Also positioning and naming, segments and personas, the competitive landscape, two voice-of-customer sources (656 Trustpilot reviews and 2,129 Hacker News comments), feasibility on Paperclip, pricing, risks and next steps.
2. [**factory-lines.md**](./factory-lines.md): what the factory makes. Line scoring, line anatomy and spec format, and Bug, Maintenance, Feature, Greenfield and Agency lines in detail. Also risk tiers and the lights-out ladder, the open line format and the public benchmark.
3. [**reliability-cost-harness.md**](./reliability-cost-harness.md) (v2): the factory harness. How coding agents fail, design principles, the factory loop and order contract, verification tiers L1–L7, and order sizing from METR horizons. Also safe-by-construction rules, reliability metrics, cost per change and per account, and Paperclip exists-vs-gap.
4. [**product-feature-strategy.md**](./product-feature-strategy.md) (v2): the CPO strategy. Voice of customer, seven bets F1–F7, the 10–100x scorecard, information architecture, a RICE backlog (beta ≈ 80 person-weeks on Paperclip), the roadmap, the reuse map, anti-features and the validation plan.
5. [**prd.md**](./prd.md) (v2): the product requirements document. Sixteen modules with numbered requirements, AI and non-functional requirements, architecture on the Paperclip fork, the data model, integrations and lead times, pricing rules, analytics, compliance, operations, the delivery plan and release gates.
6. [**marketing-plan.md**](./marketing-plan.md) (v2): go-to-market for developers, founders and agencies. Positioning, landing page, channels (X, Hacker News, GitHub, YouTube), "the factory builds the factory," SEO and AI search, the Factory Floor community, partners, the benchmark as PR, launch week, gated paid acquisition, lifecycle, budget and a 90-day calendar.
7. [**x-build-in-public-guide.md**](./x-build-in-public-guide.md) (v2): the beginner's guide to building the factory in public on X. Account setup, audiences, the weekly Factory Report, reply strategy, sharing rules for code and security, a 120-day plan and 30 ready-to-edit posts.
8. [**competitor-analysis.md**](./competitor-analysis.md): deep teardowns of Factory (factory.com), our closest competitor, and Warp Factories (open factories-as-code infrastructure, including a cost-per-PR reality check on our pricing). Also Cognition/Devin, 8090, the labs and platforms (Claude Code, Codex, Copilot, Cursor, Google, AWS), team platforms (Augment Cosmos, Amp, Tessl) and open-source factories (Symphony, Fabro). Includes a feature comparison, price comparison, threat ranking, battlecards, and recommendations C1–C12 (two need your decision).

**Reading order:**
1. The proposal (why we pivoted), then the market research (the evidence base) and the competitor analysis (who else is building this).
2. Factory lines and the harness. They define what the product does and how it stays reliable and affordable.
3. The product strategy and PRD. They turn that into a build plan.
4. The marketing plan and X guide. They turn it into a launch.
