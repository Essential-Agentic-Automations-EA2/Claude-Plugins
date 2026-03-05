---
description: Generate a filled Word (.docx) report from a template and client data. Runs fill_report.py to produce a deterministic, formatted document. Pass the template path and optionally the client name or data file.
argument-hint: [template path] [client name or reference] OR [template path] [--data path/to/data.json]
---

Generate a Word report by filling a .docx template with client and market data.

**Input:** $ARGUMENTS

## Delegation

Invoke the `report-generator` agent to handle this request end-to-end. Pass it the following context:

1. **Template path** (from arguments, or ask the user if not provided)
2. **Client name or reference** (from arguments, memory MCP, or ask the user)
3. **Data file path** (if `--data` was passed, skip data collection and use the file directly)
4. **Report type** (infer from the template name, or ask)
5. **Output directory** (default: Save the report under the client folder. if the folder does not exist, create it, or ask)

The `report-generator` agent will:
- Verify the template and identify all `{{FIELD}}` placeholders
- Pull client data from memory, portfolio files (read directly from disk), and live market data (tavily)
- Build the JSON data file
- Run `fill_report.py` to produce the document
- Report the output path and any unfilled placeholders

## Quick Mode (data file provided)

If the user passes `--data path/to/file.json`, skip straight to running the script:

```bash
python3 [plugin_scripts_path]/fill_report.py \
  --template "[template path]" \
  --data     "[data file path]" \
  --output   "[output path]"
```

---

## Template Placeholder Reference

Your Word templates should use `{{FIELD_NAME}}` syntax (uppercase, underscores).

**Standard fields available in all reports:**

| Placeholder | Description | Example |
|---|---|---|
| `{{REPORT_DATE}}` | Date the report is generated | `4 March 2026` |
| `{{REPORT_PERIOD}}` | Reporting period | `Q4 2025` |
| `{{ADVISER_NAME}}` | Adviser full name | `Sarah Chen` |
| `{{ADVISER_TITLE}}` | Adviser role | `Senior Financial Adviser` |
| `{{FIRM_NAME}}` | Firm name | `Meridian Wealth Partners` |
| `{{FIRM_AFSL}}` | AFSL number | `AFSL 123456` |
| `{{CLIENT_NAME}}` | Client full name | `James and Helen Nguyen` |
| `{{CLIENT_REFERENCE}}` | Internal client ref | `NGC-2025-0041` |
| `{{CLIENT_RISK_PROFILE}}` | Risk profile | `Balanced` |
| `{{PORTFOLIO_TOTAL_VALUE}}` | Total portfolio | `$842,300` |
| `{{PORTFOLIO_RETURN_PERIOD}}` | Return this period | `4.7%` |
| `{{RBA_CASH_RATE}}` | Current RBA rate | `4.10%` |
| `{{ASX200_LEVEL}}` | ASX 200 index level | `8,142` |
| `{{DISCLAIMER}}` | Standard disclaimer | (full text) |

See `scripts/sample_data.json` for a complete example data file.
