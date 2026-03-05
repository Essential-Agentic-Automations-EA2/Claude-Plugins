---
name: market-awareness
description: Auto-surfaces current Australian market context whenever the conversation involves investment recommendations, portfolio reviews, or product discussions. Uses tavily to retrieve live RBA cash rate, ASX 200 level, inflation figures, and sector performance so the adviser always has current context.
user-invocable: false
---

# Market Awareness

## When This Skill Activates

This skill fires automatically whenever the conversation involves:
- Investment recommendations or product comparisons
- Portfolio performance reviews
- Client briefings or meeting preparation
- Any discussion of interest rates, returns, or market conditions

Do not wait to be asked — surface current market context proactively.

## Data to Retrieve (tavily)

Run the following searches and include the results as a compact **Market Context** block:

| Data Point | Search Query |
|---|---|
| RBA cash rate | `RBA cash rate current site:rba.gov.au OR "RBA cash rate" 2025` |
| ASX 200 level | `ASX 200 index today close` |
| Australian CPI / inflation | `Australia CPI inflation rate latest ABS` |
| AUD/USD exchange rate | `AUD USD exchange rate today` |
| Sector performance | `ASX sector performance week [relevant sectors]` |
| 10-year bond yield | `Australia 10 year bond yield current` |

Retrieve only the most current figures. Always cite the source and date next to each figure.

## Output Format

Insert a **Market Context** block at the top of any response that involves market-sensitive advice:

```
---
**Market Context** (as of [date retrieved])
- RBA Cash Rate: [X]% (last changed: [date])
- ASX 200: [X,XXX] ([+/-X.X%] this week)
- CPI (latest): [X.X%] annual
- AUD/USD: [X.XXXX]
- 10-yr Bond Yield: [X.XX%]
- Sector note: [1 sentence on the most relevant sector to the current conversation]

*Sources: [cite each source URL and date]*
---
```

## Rules
- Always date-stamp the data — never present stale figures as current
- If a search returns no result, write "Data unavailable — adviser should verify before use"
- Do not fabricate or estimate market figures; only use what search returns
- Keep the block concise — it should add context, not dominate the response
