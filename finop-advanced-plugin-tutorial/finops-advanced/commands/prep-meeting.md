---
description: Generate a full client meeting briefing pack. Reads client documents directly from disk and recalls prior meeting history from memory MCP for continuity across sessions.
argument-hint: [client name] OR [client name + file path to their folder]
---

Create a complete meeting preparation pack for the following client:

$ARGUMENTS

## Step 1 — Recall Prior History (memory MCP)

Query the `memory` MCP for the client's name:
- Retrieve stored risk profile, investment goals, life stage, and any notes about preferences
- Retrieve all stored action items from prior meetings — list them with their dates
- Retrieve any recurring themes or concerns noted in previous sessions
- If nothing is found, note "No prior session history — first meeting or memory not yet populated"

## Step 2 — Read Client Documents

If a file path was provided, use the Read tool to open the client's documents:
- Look for portfolio statements, fact-find documents, and any SOA drafts
- Extract: current asset allocation, total portfolio value (if present), risk profile classification, key holdings
- If no path was provided, skip this step and proceed with conversation context only

## Step 3 — Apply Market Context

Apply the `market-awareness` skill to surface the current RBA cash rate, ASX 200 level, CPI, and relevant sector context relevant to this client's holdings.

## Step 4 — Build the Briefing Pack

---

## Client Briefing: [Client Name]
**Meeting Date:** [today's date]
**Prepared by:** Financial Adviser

---

### Client Snapshot
[2–3 sentences on who this client is, their goals, risk profile, and life stage — drawn from memory and documents]

### Prior Actions Status
[Table of open action items from memory MCP]

| # | Action | Committed Date | Status |
|---|--------|----------------|--------|
| 1 | [Action from prior meeting] | [Date stored] | Open |

If no prior actions: "No outstanding actions on record — confirm at start of meeting."

### Portfolio Focus Areas
[Key holdings or themes relevant to this client — from documents or conversation context]

### Current Market Context
[Market-awareness block: RBA rate, ASX 200, CPI, relevant sector note]

### Suggested Agenda
[Numbered agenda with time allocations, tailored to this client]

### Key Talking Points
[3–5 bullet points the adviser should raise, informed by memory, documents, and current market context]

### Questions to Ask
[3–5 open-ended questions to deepen understanding of goals or life changes]

---
*Apply compliance-language skill to all client-facing sections.*
