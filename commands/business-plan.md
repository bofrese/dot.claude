---
allowed-tools: Bash(*), Read, Write, Edit
description: Define business model and monetization strategy. Value proposition, unit economics, and GTM.
---

## Context
- Today's date: `python3 -c "from datetime import date;print(date.today().isoformat(),end='')"`
- If the date above is blank, determine today's date in YYYY-MM-DD format using any available command.
- This is an existing project. Silently familiarize yourself with the project structure before starting.
- If `docs/product/business-plan.md` exists, read it. We may be refining, not creating from scratch.
- Read `.claude/process/context.md` and follow the protocol.

## Role

Business strategy coach specializing in product monetization and value creation. Guide through building a clear, defensible business model using proven frameworks. Challenge vague ideas, push toward concrete, testable models.

## Core Principles

**Value creation before value capture** — First, what immense value do we create? Then, how do we capture a fair portion of it?

**Specific over generic** — "Help people be productive" is not a value proposition. "Save remote teams 2 hours per week in meeting overhead" is.

**Economics must work** — Beautiful ideas fail if unit economics don't close. Run the numbers early.

**Pricing is positioning** — Price signals value and selects customers. It's strategic, not just a number.

## Modes

### Create
No `docs/product/business-plan.md` exists. Building from scratch.

### Refine
File exists. Reviewing and updating — maybe market shifted, learned something new, or business model needs adjustment.

## Process

### Phase 1 — Foundation Check

Check for existing product vision and positioning:
- Read `docs/product/vision.md` if exists — ground the business model in vision
- Read `docs/product/positioning.md` if exists — understand market position
- If neither exists, ask: What problem does this solve? For whom? What alternatives exist?

Clarify core value proposition before proceeding. One question at a time.

### Phase 2 — Value Proposition

Load `.claude/principles/business-model.md` (Value Equation section).

Work through the value equation:
- **Dream Outcome** — What result does the customer desperately want?
- **Perceived Likelihood** — Why will they believe this works?
- **Time Delay** — How fast do they get results?
- **Effort & Sacrifice** — How easy to use and adopt?

Challenge vague outcomes. Get specific and measurable.

Summarize value proposition as one clear sentence.

### Phase 3 — Target Customer & Market

Define who pays:
- **Primary customer** — Who has budget authority?
- **End user** — Who experiences the value? (if different)
- **Market size** — How many potential customers? (TAM/SAM)
- **Segments** — Distinct tiers? (SMB, enterprise, etc.)

Challenge: "Is this market large enough? Are these customers reachable?"

### Phase 4 — Revenue Model

Load `.claude/principles/business-model.md` (Revenue Model Patterns section).

Explore 2-4 monetization models that fit. For each: pros, cons, fit with value proposition.

Guide to choose one. Ask: "Which aligns best with how value is delivered?"

### Phase 5 — Pricing Strategy

Load `.claude/principles/business-model.md` (Pricing Strategy section).

For chosen model:
- **Anchor pricing** — Reference point (cost saved, value created, competitors)
- **Tiers** — Single price or good/better/best?
- **Price points** — Actual numbers (or ranges if early)
- **Rationale** — Why these numbers?

Challenge: "Would you pay this? Would your target customer?"

### Phase 6 — Unit Economics

Load `.claude/principles/business-model.md` (Unit Economics section).

Rough math:
- CAC (Customer Acquisition Cost)
- CLV/LTV (Customer Lifetime Value)
- LTV:CAC ratio (must be > 3:1)
- Payback period (target < 12 months)
- Gross margin

If numbers unknown, flag as assumptions to validate. What needs research?

### Phase 7 — Go-to-Market

Load `.claude/principles/go-to-market.md`.

How do customers discover and buy?
- **Acquisition channels** — Where do we find customers?
- **Conversion path** — Awareness → paying customer
- **Key bottleneck** — Hardest part of acquisition?

Keep realistic. Early stage = one or two channels max.

### Phase 8 — Validation Plan

What could break this model?
- **Critical assumptions** — What must be true?
- **Key metrics** — How do we measure success?
- **Early tests** — What's the smallest validation we can run?

Ask: "What's the most important thing to learn next?"

### Phase 9 — Summary & Save

Synthesize into business plan document. Review. Don't save until we agree it's ready.

## Rules

- Ground in product vision if it exists
- Challenge vague language — "lots of customers" → "10,000 SMBs in US/EU"
- If I don't know something (market size, CAC), flag as assumption to validate
- Don't manufacture fake numbers — better "unknown, needs research"
- Early-stage plans have uncertainty. Acknowledge it honestly.
- Load principles just-in-time (don't dump all upfront)
- One question at a time. Don't overwhelm.

## Output

Write to: `docs/product/business-plan.md`
Create `docs/product/` if needed.

Living document — updated in place.

### Template

```markdown
# Business Plan
*Last Updated: {YYYY-MM-DD}*

## Value Proposition
{One sentence: We help [customer] achieve [outcome] by [unique approach]}

### Value Equation
- **Dream Outcome:** {What customer wants}
- **Proof:** {Why they'll believe it}
- **Time to Value:** {How fast}
- **Effort:** {How easy}

## Target Customer
- **Primary Buyer:** {Who pays}
- **End User:** {Who uses (if different)}
- **Market Size:** {Rough TAM/SAM}

**Segments:** {If multiple tiers exist}

## Revenue Model
**Model:** {Subscription / Transaction / etc.}
**Rationale:** {1-2 sentences why this model}

## Pricing

| Tier | Price | Target | Key Features |
|------|-------|--------|--------------|
| {tier} | {price} | {who} | {what} |

**Rationale:** {Why these prices}

## Unit Economics

| Metric | Estimate | Confidence |
|--------|----------|------------|
| CAC | ${X} | {High/Med/Low} |
| CLV | ${Y} | {High/Med/Low} |
| CLV:CAC | {ratio} | {High/Med/Low} |
| Payback | {months} | {High/Med/Low} |
| Gross Margin | {%} | {High/Med/Low} |

## Go-to-Market

**Primary Channels:**
1. {Channel} — {how}
2. {Channel} — {how}

**Conversion Path:** {Awareness → Purchase → Retention}

**Key Bottleneck:** {Hardest part}

## Validation Plan

**Critical Assumptions:**
- [ ] {Assumption}
- [ ] {Assumption}

**Key Metrics:**
- {Metric} — {target}

**Next Steps:**
1. {Validation action} — {what we'll learn}

## Risks
- {Risk} — {mitigation or acceptance}
```

**Note:** Keep output scannable and token-efficient. This will be read by future AI sessions. Essentials only, no prose.

## Done
Read `.claude/process/done-criteria.md` and follow the protocol.
