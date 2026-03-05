---
description: Build a retirement outcome projection for a client based on current balance, contributions, age, and risk profile. Produces compliant range-based projections with required disclaimers inline.
argument-hint: [current age] [retirement age] [current balance $] [annual contribution $] [risk profile: conservative/balanced/growth/aggressive]
---

Build a retirement income projection for the following client parameters:

$ARGUMENTS

## Step 1 — Retrieve Client Context (memory MCP)

Query `memory` for the client if a name is provided:
- Retrieve any stored retirement goals (target income, lifestyle expectations, planned retirement age)
- Retrieve existing superannuation structure or fund details if noted
- Retrieve any relevant life events (inheritance, property plans, partner details)

## Step 2 — Apply Market Context

Apply the `market-awareness` skill to surface the current RBA cash rate and 10-year bond yield — these inform the risk-free rate assumption used in projections.

## Step 3 — Compliant Projection Assumptions

Use the following ASIC-compliant assumption ranges only. Do not use optimistic single-point estimates:

| Risk Profile | Net Real Return Range (p.a.) | Scenarios |
|---|---|---|
| Conservative | 2.0% – 3.5% | Low: 2.0% / Mid: 2.75% / High: 3.5% |
| Balanced | 3.0% – 5.5% | Low: 3.0% / Mid: 4.25% / High: 5.5% |
| Growth | 4.5% – 7.0% | Low: 4.5% / Mid: 5.75% / High: 7.0% |
| Aggressive | 5.5% – 8.5% | Low: 5.5% / Mid: 7.0% / High: 8.5% |

Apply the Superannuation Guarantee (SG) rate of 11.5% (or as specified). Assume 2.5% CPI for real return calculations unless current CPI from market-awareness is materially different.

## Step 4 — Produce the Projection

---

## Retirement Projection Report
**Client:** [Name or "Client"]
**Current Age:** [X]
**Target Retirement Age:** [X]
**Years to Retirement:** [X]
**Current Balance:** $[X]
**Annual Contribution:** $[X] (employee + employer)
**Risk Profile:** [Profile]
**Report Date:** [Today's date]

> **Important disclaimer:** This projection uses modelling assumptions and is illustrative only. Actual outcomes will differ due to investment market variability, changes in tax legislation, contribution patterns, fees, and personal circumstances. This projection does not constitute financial advice. It should be read alongside a current Statement of Advice prepared by a licensed financial adviser.

---

### Projection Scenarios

| Scenario | Assumed Return | Projected Balance at Retirement | Estimated Annual Income (4% draw) | Duration at Draw Rate |
|---|---|---|---|---|
| Low (pessimistic) | X.X% p.a. | $XXX,XXX | $XX,XXX p.a. | ~XX years |
| Mid (central) | X.X% p.a. | $XXX,XXX | $XX,XXX p.a. | ~XX years |
| High (optimistic) | X.X% p.a. | $XXX,XXX | $XX,XXX p.a. | ~XX years |

*All figures in today's dollars (real terms after 2.5% CPI). Investment returns are net of an assumed 1.0% p.a. fee.*

### Age Pension Context
[Brief note on Age Pension eligibility age (currently 67), assets test thresholds, and whether projected balances suggest full/part/no pension entitlement at each scenario]

### Key Risks to Projection
- **Longevity risk:** Projection assumes retirement to age [X]. Living longer draws down capital faster.
- **Sequence-of-returns risk:** Poor early returns in retirement have a disproportionate impact. A buffer strategy may be appropriate.
- **Inflation risk:** Real returns may be lower if CPI exceeds 2.5% p.a. over the projection period.
- **Legislative risk:** Superannuation tax rules may change over the projection period.

### Contribution Sensitivity
[Show the impact of increasing annual contribution by $5,000 and $10,000 p.a. at the mid scenario]

| Scenario | Base Contribution | +$5,000 p.a. | +$10,000 p.a. |
|---|---|---|---|
| Mid projected balance | $XXX,XXX | $XXX,XXX | $XXX,XXX |

### Recommended Next Steps
1. Review superannuation fund fee structure against projected balance
2. Consider transition-to-retirement strategy if within 10 years of target retirement age
3. Reassess contribution rate if mid scenario falls below retirement income target
4. Revisit projection annually or after any significant life event

---
*Past performance is not a reliable indicator of future performance. Projections are modelling scenarios only and do not represent guaranteed outcomes. All figures in AUD. This document is general in nature and does not constitute personal financial advice. Please refer to a current Statement of Advice for personalised recommendations.*
