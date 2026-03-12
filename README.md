# Claude Plugin Tutorials

> A growing collection of Claude plugin tutorials — from simple Markdown-based plugins all the way up to MCP integrations and scripted workflows.

Welcome! This repo is your launchpad for learning how to build Claude plugins — custom AI assistants tailored to real workflows. Whether you're a business analyst, financial adviser, or just someone who wants Claude to stop being so... generic, you're in the right place.

---

## What's Inside

### [finop-basic-plugin-tutorial/](./finop-basic-plugin-tutorial/)

The starter tutorial: build a **Financial Services Plugin** from scratch using natural language and Markdown files.

| File/Folder | What it is |
|---|---|
| [workshop.pptx](./finop-basic-plugin-tutorial/workshop.pptx) | High-level overview deck — start here for the big picture |
| [lab-guide.md](./finop-basic-plugin-tutorial/lab-guide.md) | Step-by-step instructions for building your plugin |
| [finops-basic/](./finop-basic-plugin-tutorial/finops-basic/) | The starter plugin files you'll work from |
| [solution/](./finop-basic-plugin-tutorial/solution/) | The finished plugin — peek if you're stuck (no shame) |

#### What the plugin includes

- **[Commands](./finop-basic-plugin-tutorial/finops-basic/commands/)** — slash commands like `/weekly-summary`, `/draft-report`, `/prep-meeting`, and `/review-draft`
- **[Skills](./finop-basic-plugin-tutorial/finops-basic/skills/)** — reusable behaviours for compliance language and client meeting prep
- **[Agents](./finop-basic-plugin-tutorial/finops-basic/agents/)** — a compliance reviewer agent that keeps your outputs on the right side of the rules

---

## How to Get Started

1. Open the [workshop deck](./finop-basic-plugin-tutorial/workshop.pptx) to get the lay of the land
2. Follow the [lab guide](./finop-basic-plugin-tutorial/lab-guide.md) — it takes 60–90 minutes
3. When you're done, check out the [solution folder](./finop-basic-plugin-tutorial/solution/) to compare notes

**You'll need:** a paid Claude subscription (Pro, Max, Team, or Enterprise) and any text editor.

---

### [finop-advanced-plugin-tutorial/](./finop-advanced-plugin-tutorial/)

The Level 2 tutorial: extend the financial services plugin with **live market data**, **persistent client memory**, and **automated Word report generation** using MCP integrations and Python scripts.

| File/Folder | What it is |
|---|---|
| [workshop-level2.pptx](./finop-advanced-plugin-tutorial/workshop-level2.pptx) | Level 2 workshop deck — covers MCP wiring, new commands, and agents |
| [lab-guide.md](./finop-advanced-plugin-tutorial/lab-guide.md) | Step-by-step instructions for building the advanced plugin |
| [finops-advanced/](./finop-advanced-plugin-tutorial/finops-advanced/) | The complete Level 2 plugin files |

#### What the plugin adds over Level 1

- **MCP Servers** — [Tavily](https://tavily.com) for live ASX/RBA/CPI data with citations, and Memory MCP for persistent client profiles across sessions
- **New Commands** — `/portfolio-review`, `/market-briefing`, `/retirement-projection`, `/generate-report`, `/setup-test-client`
- **New Agents** — `portfolio-analyst` (drift + concentration checks), `market-researcher` (live data retrieval), `report-generator` (fills Word templates)
- **New Skill** — `market-awareness` auto-surfaces live market context in relevant conversations
- **Python Script** — `fill_report.py` fills `.docx` Word templates with live data and flags any unfilled placeholders

#### Prerequisites for Level 2

- A [Tavily API key](https://tavily.com) (free tier available)
- MCP servers registered globally: `claude mcp add`

---

## Coming Soon

- **Level 3** — bash automation, parallel sub-agent orchestration, and CRM integrations
