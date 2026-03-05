---
description: Generate a live market briefing pack using tavily. Pulls current ASX 200, sector returns, RBA cash rate, AUD/USD, and key economic releases — formatted for opening client conversations.
argument-hint: [optional: focus sectors or asset classes, e.g. "healthcare and REITs"]
---

Generate a current Australian market briefing pack for adviser use. If a sector or focus area is specified, include a dedicated section on it.

**Focus (optional):** $ARGUMENTS

## Step 1 — Delegate to Market Researcher

Invoke the `market-researcher` agent to retrieve current data. Pass it the following search brief:

- RBA cash rate and most recent decision date
- ASX 200 current level and week/month performance
- Top 3 performing and bottom 3 performing ASX sectors this week
- Australian CPI (latest ABS release) and RBA inflation target status
- AUD/USD exchange rate
- Australian 10-year government bond yield
- Any significant economic releases in the past 7 days (GDP, employment, trade balance)
- If a focus sector was specified: recent performance, key news, and notable stocks in that sector

The agent must cite sources and dates for every data point.

## Step 2 — Format the Briefing Pack

---

## Australian Market Briefing
**Prepared:** [Today's date]
**Data retrieved:** [Timestamp from agent]

---

### Key Figures at a Glance

| Indicator | Current | Change | Date |
|---|---|---|---|
| RBA Cash Rate | X.XX% | [Last change date] | [Source] |
| ASX 200 | X,XXX | [+/-X.X% WTD] | [Source] |
| AUD/USD | X.XXXX | [+/-X.X% WTD] | [Source] |
| CPI (annual) | X.X% | [vs target 2–3%] | [Source] |
| 10-yr Bond Yield | X.XX% | [+/-X bps WTD] | [Source] |

### Sector Performance (Week to Date)

**Outperformers:**
| Sector | Return WTD | Key Driver |
|---|---|---|
| [Sector 1] | +X.X% | [Brief note] |
| [Sector 2] | +X.X% | [Brief note] |
| [Sector 3] | +X.X% | [Brief note] |

**Underperformers:**
| Sector | Return WTD | Key Driver |
|---|---|---|
| [Sector 1] | -X.X% | [Brief note] |
| [Sector 2] | -X.X% | [Brief note] |
| [Sector 3] | -X.X% | [Brief note] |

### Recent Economic Releases
[Bullet list of significant data released in the past 7 days — GDP, employment, trade, retail sales — with the figure and its implication in one sentence]

### Focus: [Specified Sector, if applicable]
[Dedicated section on the requested sector: recent performance, key news, notable stocks, and adviser talking points]

### Adviser Talking Points
[3–5 ready-to-use talking points for opening a client conversation today, grounded in the data above]

### Risks to Watch
[2–3 key risks or upcoming events that advisers should be aware of this week — e.g. upcoming RBA meeting, earnings season, US Fed decision]

---
*Market data sourced from publicly available sources as at the dates noted above. This briefing is for adviser use only and does not constitute financial advice to clients. Always verify figures before use in client-facing materials.*
