# Lab Guide — Level 2: Advanced FinOps Plugin (Wealth Management)

## Overview

In Level 1 you built a pure-Markdown Claude plugin for financial advisers. In Level 2 you extend it with **MCP server integrations** that give Claude live market data, access to your client documents on disk, and persistent memory across sessions.

By the end of this lab you will have:
- A fully functional `finops-advanced` plugin with 3 MCP servers wired in
- New commands for portfolio review, live market briefings, and retirement projections
- Enhanced agents that verify regulatory requirements in real time and remember clients between sessions

Key Differences: Level 1 vs Level 2

| Feature | Level 1 (finops-basic) | Level 2 (finops-advanced) |
|---|---|---|
| MCP servers | None | tavily, memory |
| Market data | Static, from Claude's knowledge | Live, via tavily with citations |
| Client documents | Manual paste only | Read from disk via Claude Code's native tools |
| Client history | Starts fresh each session | Persists via memory MCP |
| Compliance verification | Knowledge-based | Verified against ASIC.gov.au in real time |
| New commands | — | portfolio-review, market-briefing, retirement-projection |
| New agents | — | portfolio-analyst, market-researcher |
| New skills | — | market-awareness |

---

## Prerequisites

| Requirement | Notes |
|---|---|
| Claude Code CLI | `claude --version` should work |
| A free Tavily API key | https://app.tavily.com/ — takes ~2 minutes |
| Some sample client documents | PDFs, CSVs, or text files — can be dummy data |

---

## Part 1 — Setup

Two steps: register the MCP servers once globally, then launch Claude Code with the plugin directory on every session.

### Step 1 — Register MCP servers (one-time)

`--plugin-dir` loads commands and agents but does **not** read `.mcp.json` from the plugin folder. MCP servers must be registered globally:

```bash
# Set your API key first
export TAVILY_API_KEY=your_key_here   # add to ~/.zshrc or ~/.bashrc for persistence

### Step 2 — Launch with the plugin (every session)

```bash
claude --plugin-dir /path/to/level2/plugin-level2/finops-advanced

# for example
claude --plugin-dir /media/daghan/DATA/Daghan/git/EDA-repository/agent-experiments/claudeplugin/level2/plugin-level2/finops-advanced
```

```powershell
# Windows
claude --plugin-dir C:\path\to\level2\plugin-level2\finops-advanced
```

Verify the servers loaded:

```
/mcp
```

You should see: `tavily`, `memory`.

---

## Part 2 — Plugin Structure Walkthrough

```
plugin-level2/finops-advanced/
├── .claude-plugin/plugin.json   ← Plugin metadata (v2.0)
├── .mcp.json                    ← MCP server configuration
│
├── skills/
│   ├── compliance-language/     ← Enhanced: tavily for ASIC lookups
│   ├── client-meeting-prep/     ← Enhanced: native file reading + memory integration
│   ├── email-tone/              ← Unchanged from v1
│   └── market-awareness/        ← NEW: auto-surfaces live market context
│
├── commands/
│   ├── draft-report.md          ← Enhanced: reads portfolio files
│   ├── prep-meeting.md          ← Enhanced: memory recall + document reading
│   ├── weekly-summary.md        ← Enhanced: memory cross-reference
│   ├── review-draft.md          ← Unchanged
│   ├── summarise-meeting.md     ← Unchanged
│   ├── portfolio-review.md      ← NEW: full portfolio analysis
│   ├── market-briefing.md       ← NEW: live ASX/RBA briefing pack
│   ├── retirement-projection.md ← NEW: compliant retirement modelling
│   ├── generate-report.md       ← NEW: fills Word template via Python script
│   └── setup-test-client.md     ← NEW: creates demo client folder + portfolio.txt
│
├── agents/
│   ├── compliance-reviewer.md   ← Enhanced: real-time ASIC verification
│   ├── meeting-summariser.md    ← Enhanced: stores to memory
│   ├── portfolio-analyst.md     ← NEW: reads + analyses portfolio files
│   ├── market-researcher.md     ← NEW: live market data via tavily
│   └── report-generator.md      ← NEW: collects data + runs fill_report.py
│
└── scripts/
    ├── fill_report.py           ← Replaces {{PLACEHOLDERS}} in .docx templates
    └── sample_data.json         ← Sample payload for testing the script
```

---

## Part 3 — What the MCP Servers Do


### Native File Tools — Client Document Access
Claude Code reads files directly from disk. Used by:
- `/portfolio-review` — reads portfolio statement files
- `/prep-meeting` — reads client fact-find documents and SOA drafts
- `/draft-report` — reads portfolio data when a file path is provided

**Exercise:** Run the setup command to create the demo client folder and portfolio file automatically:
```
/finops-advanced:setup-test-client
/clear 
```

/clear clears the context so that portfolio information is no longer in the memory and needs to be read again

Then run:
```
/finops-advanced:portfolio-review ~/Documents/clients/smith-jane/portfolio.txt balanced
```

### `tavily` — Live Market Data
Gives Claude the ability to search the web for current market information. Used by:
- `/finops-advanced:market-briefing` — pulls live ASX, RBA, CPI, sector data
- `compliance-reviewer` agent — verifies current ASIC regulatory requirements
- `market-researcher` agent — retrieves data for briefing packs
- `market-awareness` skill — auto-surfaces context in relevant conversations

**Exercise:** Run:
```
/finops-advanced:market-briefing healthcare and technology sectors
```
Observe how the agent cites sources and dates next to every figure.

### `memory` — Client Continuity
Gives Claude a persistent knowledge graph that survives across sessions. Used by:
- `meeting-summariser` agent — stores action items after every meeting
- `/finops-advanced:prep-meeting Jane Smith` — recalls prior action items and client context

After that we will simulate a meeting note added to the memory

```bash 
/finops-advanced:summarise-meeting Jane Smith — meeting 3 Mar. Discussed CBA concentration risk.                                                                                                                           
  Action: adviser to prepare rebalancing options by 10 Mar.       

``` 

On a new claude 

```bash
claude --plugin-dir /path/to/level2/plugin-level2/finops-advanced

# for example
claude --plugin-dir /media/daghan/DATA/Daghan/git/EDA-repository/agent-experiments/claudeplugin/level2/plugin-level2/finops-advanced
```

write the following  

- `/finops-advanced:weekly-summary Jane Smith` — surfaces recurring themes and carried-over actions
- `/finops-advanced:prep-meeting Jane Smith` — recalls prior action items and client context

---

## Part 4 — Hands-On Cheat Sheet

### Exercise 1: Portfolio Review
```
/finops-advanced:portfolio-review ~/Documents/clients/smith-jane/portfolio.txt balanced
```
What to observe:
- Claude reads the file using its native Read tool (no MCP needed)
- Allocation vs target table is generated
- Concentration flags appear for any holding over 10%
- Current RBA rate and ASX 200 appear in the market context block

### Exercise 2: Live Market Briefing
```
/finops-advanced:market-briefing
```
Then with a sector focus:
```
/finops-advanced:market-briefing REITs and infrastructure
```
What to observe:
- Every data point includes a source URL and date
- The adviser talking points are grounded in the retrieved data
- Data gaps are explicitly noted rather than estimated

### Exercise 3: Retirement Projection
```
/finops-advanced:retirement-projection 48 65 320000 18000 growth
```
What to observe:
- Three scenarios (low/mid/high) with distinct return assumptions
- All projections in today's dollars (real terms)
- Required disclaimers appear inline — not as an afterthought
- Contribution sensitivity table shows the impact of saving more

### Exercise 4: Memory Continuity
1. Run `/summarise-meeting` with notes that include a client named "Jane Smith" and action items
2. Close and reopen Claude Code (new session)
3. Run `/prep-meeting Jane Smith`
4. Observe that prior action items and client context are recalled from memory

### Exercise 5: Compliance Verification
```
/review-draft [paste a draft client email with some borderline language]
```
What to observe (with Tavily key configured):
- The compliance-reviewer agent first searches ASIC.gov.au to verify current requirements
- The report cites the search date and notes any regulatory updates
- Issues are flagged with suggested replacement language

---

## Part 5 — Generate Report

The `generate-report` command produces a filled Word (`.docx`) document from a template. It delegates to the `report-generator` agent, which gathers all data, builds a JSON payload, and runs `scripts/fill_report.py`.

### How it works

1. You provide a `.docx` template containing `{{FIELD_NAME}}` placeholders
2. The `report-generator` agent collects data from three sources:
   - **memory MCP** — client risk profile, goals, meeting history
   - **Portfolio file** — read directly from disk
   - **tavily** — live RBA rate, ASX 200, CPI
3. The agent runs `fill_report.py` to produce the final document

### Usage

!Copy NGC-2025-0041_Q4-2025_quarterly-review.docx to ~/Documents/clients/templates

**Quick mode** — skip data collection, use a pre-built JSON file:
```
/finops-advanced:generate-report ~/Documents/clients/templates/NGC-2025-0041_Q4-2025_quarterly-review.docx --data scripts/sample_data.json
```

**Full mode** — agent gathers all data automatically:
```
/finops-advanced:generate-report ~/Documents/clients/templates/NGC-2025-0041_Q4-2025_quarterly-review.docx Jane Smith
```



### Template placeholder format

Use `{{UPPERCASE_WITH_UNDERSCORES}}` in your Word template. Key placeholders:

| Placeholder | Example value |
|---|---|
| `{{CLIENT_NAME}}` | `James and Helen Nguyen` |
| `{{CLIENT_RISK_PROFILE}}` | `Balanced` |
| `{{PORTFOLIO_TOTAL_VALUE}}` | `$842,300` |
| `{{RBA_CASH_RATE}}` | `4.10%` |
| `{{ASX200_LEVEL}}` | `8,142` |
| `{{REPORT_DATE}}` | `4 March 2026` |
| `{{ADVISER_NAME}}` | `Sarah Chen` |
| `{{DISCLAIMER}}` | *(standard disclaimer text)* |

See `scripts/sample_data.json` for the full list of supported fields.

### Output naming

The script names output files as: `[CLIENT_REF]_[PERIOD]_[TYPE].docx`

### What to observe
- The agent reports the output file path on completion
- Any `{{PLACEHOLDERS}}` that could not be filled are listed so you can supply missing data
- Running with `--data sample_data.json` is a fast way to verify a new template works before wiring up live data

---

## Part 6 — Troubleshooting

### "MCP server not found" errors
```bash
claude mcp list          # Check what's registered
claude mcp remove [name] # Remove and re-add if needed
```

### tavily returns no results
- Confirm your API key is set: `echo $TAVILY_API_KEY`
- Re-register with the real key (see Part 2)
- Check your Tavily API quota at https://app.tavily.com/

### Claude can't find a client file
- Make sure you're providing an absolute path (e.g. `~/Documents/clients/smith/portfolio.txt`)
- Claude Code's Read tool can access any file the current user can read — no MCP registration needed

### memory doesn't persist between sessions
- Confirm the memory MCP is registered: `claude mcp list`
- Memory is stored in a local knowledge graph — it persists as long as the MCP server data directory is intact
- If you reinstalled, you may need to rebuild memory entries

---

## Summary

In Level 2 you have:

1. **Extended a Markdown plugin with MCP servers** — no custom code required, just configuration
2. **Wired live market data** into adviser workflows using Tavily
3. **Read client documents from disk** using Claude Code's native file tools — no extra MCP needed
4. **Created persistent client memory** that survives across Claude Code sessions
5. **Built compliant, data-grounded commands** for portfolio review, retirement modelling, and market briefings

The key insight: **only add an MCP server when Claude doesn't already have the capability**. File access, bash execution, and code editing are built into Claude Code — MCP adds things Claude can't do natively, like live web search (Tavily), persistent cross-session memory, and Gmail.
