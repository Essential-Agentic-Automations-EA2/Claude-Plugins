---
description: Read a client's portfolio statement file and produce a structured review against their risk profile — including drift warnings, concentration flags, and rebalancing suggestions with compliant language.
argument-hint: [file path to portfolio statement] [client risk profile: conservative/balanced/growth/aggressive]
---

Conduct a full portfolio review for the following input:

$ARGUMENTS

## Step 1 — Read Portfolio Document

Use the Read tool to open the portfolio statement file provided:
- Extract: asset class breakdown (equities, fixed income, cash, alternatives, property), individual holdings, and any performance figures present
- Identify the total portfolio value and reporting date
- If no file path is given, ask the user to provide one or paste the portfolio data directly

## Step 2 — Retrieve Client Context (memory MCP)

Query `memory` for the client associated with this portfolio:
- Retrieve stated risk profile (if not already provided in arguments)
- Retrieve investment goals, time horizon, and any known constraints (e.g., ethical screens, liquidity needs)
- Retrieve target allocation if previously stored

## Step 3 — Apply Market Context

Apply the `market-awareness` skill to surface current RBA cash rate, ASX 200 level, and sector context relevant to the portfolio's holdings.

## Step 4 — Delegate Analysis

Invoke the `portfolio-analyst` agent to perform the detailed analysis, passing it:
- The extracted portfolio data
- The client's risk profile and target allocation
- Current market context

## Step 5 — Produce the Review Report

---

## Portfolio Review Report
**Client:** [Name from document or memory]
**Portfolio Value:** [Total as at reporting date]
**Reporting Date:** [From document]
**Risk Profile:** [conservative / balanced / growth / aggressive]
**Reviewed:** [Today's date]

---

### Current Allocation vs Target

| Asset Class | Current % | Target % | Drift | Status |
|---|---|---|---|---|
| Australian Equities | X% | X% | +/-X% | ✅ Within band / ⚠️ Drift / ❌ Significant drift |
| International Equities | X% | X% | +/-X% | |
| Fixed Income | X% | X% | +/-X% | |
| Cash | X% | X% | +/-X% | |
| Property / Infrastructure | X% | X% | +/-X% | |
| Alternatives | X% | X% | +/-X% | |

*Drift bands: ±5% trigger review; ±10% trigger rebalance recommendation.*

### Concentration Risk Flags
[List any single holding exceeding 10% of portfolio, or any sector exceeding 30% of equity allocation]
- ⚠️ [Holding/Sector]: [X%] of portfolio — exceeds recommended concentration limit

### Market Context
[Market-awareness block relevant to this portfolio's major exposures]

### Rebalancing Suggestions
[Specific, compliant rebalancing actions. Use "may be appropriate to consider" language.]

> The following suggestions are general in nature and do not constitute personal financial advice. Please review the client's current Statement of Advice and consult the client before implementing any changes.

| Action | Rationale | Priority |
|---|---|---|
| Reduce [Holding] by ~$X | Concentration above threshold | High |
| Increase [Asset Class] by ~$X | Underweight vs target | Medium |

### Fee Drag Assessment
[If fee data is present in the document, note total fee drag as a % of portfolio. Flag if above 1.5% p.a.]

### Recommended Next Steps
1. [Action 1 with owner and suggested timeframe]
2. [Action 2]
3. [Action 3]

---
*Past performance is not a reliable indicator of future performance. All figures are in AUD unless otherwise stated.*
*This review is general in nature. Any recommendations must be considered in the context of a current Statement of Advice.*
