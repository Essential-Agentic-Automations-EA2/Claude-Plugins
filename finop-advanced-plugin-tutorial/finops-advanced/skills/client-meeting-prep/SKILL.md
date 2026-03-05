---
name: client-meeting-prep
description: Helps financial advisers prepare for client meetings. Enhanced in v2 to read client documents using Claude Code's native file tools and recall prior meeting history from memory MCP. Use when asked to prepare for a meeting, review a client, or get a briefing on someone.
user-invocable: false
---

# Client Meeting Preparation

When preparing for a client meeting, follow these steps in order:

## 1. Recall Prior History (memory MCP)

Before anything else, query memory for this client:
- Search memory for the client's name to retrieve stored risk profile, investment goals, and prior meeting action items
- Surface any recurring themes or unresolved items from past sessions
- If no memory entries exist, note this and prepare to capture key facts after the meeting

## 2. Read Client Documents

Use the Read tool to open available client documents:
- Look for portfolio statements, SOA drafts, or fact-find documents under the client's folder
- Extract: current allocation summary, stated risk profile, significant holdings, any flagged concerns
- If no documents are found, proceed with information provided in conversation and note the gap

## 3. Client Context Summary
- Combine memory recall and document findings into a single client snapshot
- Identify key financial goals, risk profile, and current portfolio focus
- List any open action items from previous meetings (from memory MCP)

## 4. Meeting Agenda Structure
Always suggest a structured agenda:
1. Relationship check-in (5 min)
2. Portfolio performance review (10 min)
3. Market updates relevant to their holdings (10 min)
4. New recommendations or actions (15 min)
5. Next steps and follow-up items (5 min)

## 5. Talking Points
Prepare 3–5 concise talking points tailored to:
- Current market conditions relevant to the client's sector exposure
- Any life events or circumstances they have mentioned (from memory)
- Upcoming regulatory or tax deadlines

## 6. Output Format
Always produce:
- A one-page briefing document
- A bullet-point agenda the adviser can print
- A list of questions to ask the client
- A "Prior Actions Status" section showing outstanding items from memory

## Tone
- Professional but warm
- Use plain English, avoid jargon unless the client is sophisticated
- Always frame recommendations in terms of the client's stated goals
