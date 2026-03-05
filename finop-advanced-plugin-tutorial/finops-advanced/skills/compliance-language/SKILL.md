---
name: compliance-language
description: Ensures all client-facing communication uses compliant, regulator-approved language. Use automatically whenever drafting emails, reports, or summaries for clients. Enhanced in v2 with tavily to verify current ASIC/AFCA requirements before finalising any compliance-sensitive output.
user-invocable: false
---

# Compliance Language Guidelines

## MCP Integration (v2 Enhancement)

Before applying compliance rules to any client-facing document, use `tavily` to verify the current status of any cited regulatory guidance:
- Search: `"ASIC RG 175" OR "ASIC RG 244" site:asic.gov.au` to confirm current SOA/FSG requirements
- Search: `"AFCA" complaints latest guidance` if the document involves dispute or complaint language
- Search: `"ASIC" [specific regulation referenced]` if a specific rule is cited in the draft

Only proceed with compliance review after confirming the cited guidance is still current. If search results indicate a regulatory update, note it prominently in your output.

## Always Include
- Appropriate disclaimers when discussing investment performance
- "Past performance is not indicative of future results" when referencing historical returns
- "This information is general in nature and does not constitute financial advice" on general communications

## Never Include
- Guaranteed return language (e.g., "you will earn", "guaranteed growth")
- Comparisons to specific competitor products by name
- Specific predictions about market movements stated as fact

## Required Disclosures by Communication Type

### Client Emails
Add at the bottom:
> This email contains general information only and does not take into account your personal financial situation. Please consult a licensed financial adviser before making any investment decisions.

### Performance Reports
Add at the top:
> Past performance is not a reliable indicator of future performance. All figures are in AUD unless otherwise stated.

### Product Recommendations
Add inline before the recommendation:
> The following information is provided for educational purposes. Please review the relevant Product Disclosure Statement (PDS) before investing.

### Statements of Advice (SOA)
Verify against current ASIC RG 175 requirements via tavily before finalising. At minimum include:
- Subject matter of the advice
- Basis for the advice
- Any conflicts of interest
- Remuneration disclosure

## Tone Rules
- Use "may" and "could" instead of "will" and "shall" for forward-looking statements
- Replace "best" with "suitable" or "appropriate for your situation"
- Avoid superlatives in investment contexts
- Use "general advice warning" phrasing where required under the Corporations Act 2001
