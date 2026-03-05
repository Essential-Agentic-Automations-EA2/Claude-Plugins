---
description: Send a draft communication to the Compliance Reviewer agent for a full compliance check
argument-hint: [paste your draft text here]
---

Pass the following draft to the compliance-reviewer agent for a full compliance review:

$ARGUMENTS

The agent will:
1. Check all forward-looking language
2. Verify performance disclaimers are present
3. Review regulatory compliance for Australian financial services
4. Return a structured report with any issues and a corrected version

After the agent returns its report:
- If status is ✅ PASS: confirm the draft is ready to send
- If status is ⚠️ PASS WITH CHANGES: present the corrected version and highlight what changed
- If status is ❌ FAIL: clearly explain what must be fixed before the content can be used

Always end with: "Would you like me to apply the suggested changes and produce a final version?"
