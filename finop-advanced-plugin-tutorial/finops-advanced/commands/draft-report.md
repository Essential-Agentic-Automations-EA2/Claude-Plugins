---
description: Draft a client-ready financial summary report. Can read a portfolio statement file directly when a file path is provided. Pass either raw notes or a file path.
argument-hint: [file path to portfolio statement] OR [paste raw notes or data]
---

Draft a polished, client-ready financial summary report using the input below. Apply all compliance language standards including required disclaimers, forward-looking language rules, and disclosure requirements.

**Input:**
$ARGUMENTS

## Step 1 — Resolve Input

If the input looks like a file path (starts with `/`, `~/`, or `./`):
- Use the Read tool to read the file at that path
- Extract portfolio data, performance figures, and any client details from the document
- Note the file name and date in the report header

If the input is pasted notes or data, use it directly.

## Step 2 — Apply Market Context

Apply the `market-awareness` skill to surface the current RBA cash rate, ASX 200 level, and relevant sector context. Include this as a **Market Context** block before the Market Commentary section.

## Step 3 — Draft the Report

Structure your output as:

---

## Financial Summary Report
**Prepared for:** [Client Name if known, otherwise "Valued Client"]
**Period:** [Infer from context or use current quarter]
**Date:** [Today's date]
**Source document:** [File name if read from disk, otherwise "Adviser-provided notes"]

---

### Executive Summary
[2–3 sentences summarising key outcomes for the period]

### Portfolio Performance
[Summarise performance data with compliant language — no guaranteed return language, past performance disclaimer required]

> Past performance is not a reliable indicator of future performance. All figures are in AUD unless otherwise stated.

### Market Context
[Insert market-awareness block here]

### Market Commentary
[Brief relevant market context — 1 paragraph, linked to the client's actual holdings]

### Recommendations
[Any actions or adjustments suggested, with compliance disclaimers inline. Reference PDS where products are named.]

### Next Steps
[Numbered list of agreed actions]

---
*All forward-looking statements use "may", "could", or "is expected to" language per compliance-language skill.*
*This report contains general information only and does not constitute personal financial advice.*
