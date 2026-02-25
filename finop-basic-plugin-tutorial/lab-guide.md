# Building Claude Plugins for Financial Services
## Level 1 Lab Guide — No Code Required

*Building a Financial Services Plugin with Natural Language*

**Time estimate:** 60–90 minutes  
**Audience:** Business analysts, financial advisers, operations staff, anyone who uses Claude daily  
**Goal:** Build and test a working plugin using only Markdown and a text editor  
**Next:** When you're done here, continue with the Level 2 guide to add MCP tools and sub-agent orchestration.

---

## Before You Start

**What you need:**
- A paid Claude subscription (Pro, Max, Team, or Enterprise)
- A text editor (VS Code, Notepad++, nano, or any editor you prefer)
- The workshop plugin files — unzip `plugin-files.zip` to a folder of your choice

---

### Platform Setup

Follow the instructions for your operating system.

---

#### 🍎 macOS

Install Claude Desktop, then enable Cowork from the sidebar. Plugins can also be built and tested via Claude Code in Terminal.

**Install Claude Code (recommended for building):**
```bash
npm install -g @anthropic-ai/claude-code
claude --version
```

**Or use Cowork directly:**  
Open Claude Desktop → Cowork tab → Plugins → Upload Plugin

---

#### 🪟 Windows

Install Claude Desktop (latest version required for Cowork). Plugins can be uploaded directly in the Cowork tab or tested via Claude Code in PowerShell or Windows Terminal.

**Install Claude Code:**
```powershell
npm install -g @anthropic-ai/claude-code
claude --version
```

> **Note:** Windows arm64 is not supported by Cowork. If you are on an arm64 device, use Claude Code exclusively for this workshop.

**Or use Cowork directly:**  
Open Claude Desktop → Cowork tab → Plugins → Upload Plugin

---

#### 🐧 Linux*

> **\* Linux note:** Claude Cowork (the desktop app) is not available on Linux. However, **Claude Code runs natively on Linux** and uses the **same plugin format** as Cowork — everything you build here is fully compatible. You will use Claude Code throughout this workshop instead of the Cowork UI.

**Install Claude Code:**
```bash
npm install -g @anthropic-ai/claude-code
claude --version
```

All testing is done via the `claude` terminal command with the `--plugin-dir` flag. There is no Cowork desktop app to install.

---

### All Platforms: Get the Workshop Files

```bash
git clone https://github.com/EDA-repository/finops-claude-plugins
cd finops-plugins
```

Or unzip the downloaded `plugin-files.zip` to a folder of your choice.

---

## What You'll Build

A plugin called **FinOps Basic** that turns Claude into a financial services specialist with:
- Automatic compliance language on everything it writes
- A `/prep-meeting` command that generates a full client briefing pack
- A `/draft-report` command that produces polished, compliant client reports
- A `compliance-reviewer` sub-agent that independently audits drafts before they leave your desk

---

## Module 1.1 — Understanding Plugin Structure

A Claude plugin is just a folder with a specific layout:

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json        ← tells Claude what this plugin is
├── skills/
│   └── my-skill.md        ← knowledge Claude uses automatically
├── commands/
│   └── my-command.md      ← slash commands you trigger manually
└── agents/
    └── my-agent.md        ← specialist sub-agents you delegate to
```

**The golden rule:** Skills fire automatically when relevant. Commands fire when you type `/command-name`. Agents are invoked by commands or skills to handle a specific focused task.

---

## Module 1.2 — Explore the Sample Plugin

Open the `level1-finops-basic` folder and read each file:

1. `.claude-plugin/plugin.json` — the plugin identity card
2. `skills/compliance-language.md` — rules Claude follows automatically on all output
3. `skills/client-meeting-prep.md` — the meeting prep workflow
4. `commands/prep-meeting.md` — slash command definition
5. `commands/draft-report.md` — second slash command
6. `commands/review-draft.md` — third slash command that delegates to the compliance agent
7. `agents/compliance-reviewer.md` — the sub-agent that reviews drafts

**Discussion questions:**
- What would happen if you removed the compliance skill? How would Claude behave differently?
  - The weekly-summary, draft-report, and prep-meeting commands would produce outputs without disclaimers unless the prompt template itself includes them
  - The /review-draft command would still catch problems — but only if someone remembered to run it
  - Claude's general training gives it some awareness of financial compliance, but it is not firm-specific and would not produce your exact required disclosure text
  - The skill creates a default-safe posture — compliance is the path of least resistance. Without it, compliance becomes opt-in, depending on the user running /review-draft or manually requesting disclaimers. In a regulated context, that's the difference between guardrails and guidelines. Removing it doesn't break the plugin — it just shifts responsibility from the system to the user.
- Why is `prep-meeting` a command rather than a skill?
    - Why prep-meeting has to be a command
        - It needs a target. The command takes $ARGUMENTS — the client name or pasted notes. Without that, there's nothing to act on. Claude cannot know unprompted which client you're preparing for, when the meeting is, or what to include. The user must supply context, so the user must initiate it.
        - It produces a primary deliverable. The output is the entire point — a formatted briefing pack. That's a document the user explicitly requests, not a background behaviour that quietly improves other outputs.
        - It would be disruptive as a skill. Imagine if meeting prep fired automatically every time a client name was mentioned — it would generate unsolicited briefing packs mid-conversation. Skills should be invisible; commands should be visible.
    - Why compliance-language has to be a skill
      -It has no meaningful trigger point a user would invoke — you don't decide to write compliantly, you just always should. Making it a command would require users to remember to run /compliance-language before every draft, which defeats the purpose entirely. Its value is that it's silent and always-on.

---
  The design rule
  - Commands = "Do this thing now, with this input."
  - Skills = "Always behave this way, without being asked."
---


## Module 1.3 — Test the Sample Plugin

**macOS / Windows — Option A: Test via Cowork**
1. Open Claude Desktop → Cowork tab → Plugins → Upload Plugin
2. Select the `level1-finops-basic` folder (or zip it first)
3. Once installed, start a Cowork session

**All platforms — Option B: Test via Claude Code (recommended for building)**
```bash
claude --plugin-dir ~/plugin-level1/finops-basic
```
> **Linux users:** this is your only option — use Claude Code.

Once the plugin is loaded, try these prompts:

**Test 1 — Does the compliance skill fire automatically?**
```
Write a short email to a client telling them their portfolio returned 12% last year
and will definitely return 15% next year.
```
👀 Watch what Claude does. Does it correct the "definitely" language?

**Test 2 — Test the prep-meeting command:**
```
/finops-basic:prep-meeting Sarah Chen — retail investor, $250K portfolio, moderate risk, 
focused on ASX blue chips and some international exposure. 
Last meeting we discussed rebalancing away from banks.
```

**Test 3 — Test the draft-report command:**
```
/finops-basic:draft-report Q4 2024: Portfolio up 8.2% vs ASX 200 up 6.1%. 
Top performers: BHP +18%, CSL +12%. Underperformers: TLS -4%. 
Cash position at 8%, slightly elevated.
```

---

## Module 1.4 — Customise the Plugin

Now make it your own. Pick **one** of these exercises.

> **Tip — Let Claude write it for you.** You can use Claude itself (in a separate terminal session, outside the plugin session) to draft new skills and commands interactively. See the [Interactive Skill Creation](#interactive-skill-creation-with-claude) section below for the exact prompts to use.

---

### Exercise A — Add a New Skill

Skills live in subdirectories under `skills/`, each containing a `SKILL.md` file.

Create the folder and file:
```
skills/
└── email-tone/
    └── SKILL.md       ← create this
```

The `SKILL.md` should start with frontmatter then your instructions:

```markdown
---
name: email-tone
description: Guides the tone and structure of all client emails. Apply automatically when drafting any client email.
user-invocable: false
---

# Email Tone Guidelines
...your rules here...
```

Write a skill that tells Claude how emails at your organisation should sound. Include:
- Preferred greeting style
- Tone guidance (formal/conversational)
- How to close emails
- Any specific phrases your team uses or avoids

### Exercise B — Add a New Command

Commands are flat `.md` files in the `commands/` folder. The filename becomes the command name.

Create:
```
commands/
└── weekly-summary.md       ← create this
```

The file should start with:
```markdown
---
description: Summarise a week of client interactions into a structured team report
argument-hint: [paste client interaction notes]
---

...your instructions here...
```

This creates a `/finops-basic/weekly-summary` command that takes a list of client interactions from the week and produces a structured summary report for a team meeting.

before you may want to create some client data in a differnt folder. Ask claude to create some realistic client logs such as meeting in a folder and give that folder name such as "/finops-basic:weekly-summary [client data folder location]"

### Exercise C — Customise Compliance Rules

Edit `skills/compliance-language/SKILL.md` to add:
- Your organisation's actual disclaimer text
- Any product-specific language rules
- Region-specific requirements (e.g., ASIC-specific wording for Australian clients)

---

### Interactive Skill Creation with Claude

The fastest way to build a new skill is to describe what you want to Claude and have it write the `SKILL.md` for you. Open a **new terminal session** (separate from the plugin session) and run:

```bash
claude
```

Then paste this prompt, filling in your specifics:

```
I'm building a Claude Code plugin for a financial services firm.
I need a new skill file at:
  skills/email-tone/SKILL.md

The skill should fire automatically whenever Claude drafts a client email.
It should NOT be user-invocable (background knowledge only).

Our email tone guidelines are:
- Always open with "Dear [First Name],"
- Conversational but professional — no jargon
- Close with "Kind regards, [Your Name]"
- Never use urgency language like "act now" or "don't miss out"
- Always include our standard disclaimer at the bottom

Please write the complete SKILL.md file including correct frontmatter.
```

Claude will output the complete file. Copy it into the correct location:
```
skills/email-tone/SKILL.md
```

Once copied, reload the plugin and test the skill by asking Claude to draft a client email without mentioning tone at all:
```
Draft an email to James telling him his portfolio is up 6% this quarter.
```

Because `user-invocable: false` is set, the skill fires silently in the background — Claude should automatically open with "Dear James,", avoid jargon, close with "Kind regards," and append the disclaimer, all without being asked.

You can use the same approach to create commands — just change the prompt to describe the command behaviour and ask for the file to go in `commands/weekly-summary.md`.

---

## Module 1.5 — Test Your Customisation

After making your changes, reload the plugin:

**Via Claude Code (all platforms including Linux):**
```bash
# Exit current session and relaunch
claude --plugin-dir ~/plugin-level1/finops-basic
```

**Via Cowork (macOS / Windows):**  
Go to Plugins → your plugin → click the refresh/re-upload button, then start a new Cowork session.

Test that your changes work as expected. Did the new skill or command behave the way you intended?

---

## Module 1.6 — Introduction to Sub-Agents

Sub-agents are specialised Claude instances that your plugin can delegate specific tasks to. Think of them as hiring a specialist: instead of asking your generalist assistant to also be your compliance officer, you spin up a dedicated compliance reviewer who does only that job — thoroughly, consistently, every time.

**Why sub-agents?**
- They have a tightly scoped system prompt, so they stay focused
- They can be invoked by commands or skills when needed
- They return structured output that the main Claude incorporates into its response
- They make complex workflows predictable and auditable

### Sub-Agent File Location

Sub-agents live in an `agents/` folder at the plugin root:

```
my-plugin/
├── .claude-plugin/plugin.json
├── skills/
├── commands/
└── agents/
    └── compliance-reviewer.md   ← your sub-agent
```

### Explore the Sample Sub-Agent

Open `agents/compliance-reviewer.md` in the Level 1 plugin. Notice:
- The YAML frontmatter includes `model:` — you specify which Claude model handles this agent
- The system prompt is very focused: it only reviews, never drafts
- The output format is rigidly defined so the parent can parse it reliably

### Test the Sub-Agent via the /review-draft Command

**macOS / Windows — via Cowork:**  
Ensure the `level1-finops-basic` plugin is installed in Cowork, start a session, then type `/review-draft`.

**All platforms — via Claude Code:**
```bash
claude --plugin-dir ./plugin-files/level1-finops-basic
```
> **Linux users:** use Claude Code as above.

Try this prompt to invoke the compliance reviewer agent:
```
/finops-basic:review-draft 

Dear Sarah,

Your portfolio has had an incredible year and will definitely continue 
to outperform the market. I guarantee you'll see at least 12% returns 
next year based on our best-in-class strategy.

Regards,
James
```

Watch how the compliance-reviewer agent independently catches every issue and returns a structured report — then the main Claude synthesises that into a response to you.

**Discussion question:** Why is it better to have a separate agent review the content rather than just asking the main Claude to "also check for compliance issues"?
- Asking the main Claude to self-review is like asking a lawyer to proofread their own contract. Technically possible, practically unreliable. A separate agent with a single role, a fixed checklist, and no authorial attachment is structurally incapable of the biases that make self-review weak.

### Level 1 Sub-Agent Exercise

Create sub-agent. Add a file `finps-basic/agents/meeting-summariser.md` that:
- Has a focused role: summarising meeting notes into a structured format
- Defines an exact output format (agenda recap, decisions made, action items with owner and deadline)
- Is invoked by a new `/summarise-meeting` command you also create

Copy above to claude and relaod your plugin. and now test 

```
/finops-basic:summarise-meeting Sarah Chen — retail investor, $250K portfolio, moderate risk, 
focused on ASX blue chips and some international exposure. 
Last meeting we discussed rebalancing away from banks.
```

---

## Module 1.7 — Package and Share

When you're happy with your plugin, package it to share with your team:

**macOS / Linux:**
```bash
cd plugin-files
zip -r finops-basic-myplugin.zip level1-finops-basic/
```

**Windows (PowerShell):**
```powershell
Compress-Archive -Path level1-finops-basic -DestinationPath finops-basic-myplugin.zip
```

Your colleagues on **macOS or Windows** can upload it in the Cowork app via **Plugins → Upload Plugin**.  
Your colleagues on **Linux** can load it with `claude --plugin-dir ./level1-finops-basic`.

---

## Next Steps

- ✅ **Level 1 complete!**
- Continue to the **Level 2 guide** to add MCP tool connections, live market data, a bash data pipeline, and multi-agent orchestration.
- Or explore the [official Anthropic plugin examples](https://github.com/anthropics/knowledge-work-plugins) on GitHub for more inspiration.

---

*Workshop materials: github.com/EDA-repository/finops-claude-plugins*
*Questions? Post in the workshop Slack channel or raise a GitHub issue.*
