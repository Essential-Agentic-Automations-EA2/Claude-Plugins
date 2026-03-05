---
description: Create a demo client folder and portfolio file for testing the portfolio-review command.
argument-hint: [optional: client name slug, defaults to smith-jane]
---

Set up a demo client directory and portfolio file for testing.

$ARGUMENTS

## Step 1 — Determine Client Slug

Use the argument if provided, otherwise default to `smith-jane`.

## Step 2 — Create Client Folder and Portfolio File

Use the Bash tool to run:

```bash
mkdir -p ~/Documents/clients/smith-jane
cat > ~/Documents/clients/smith-jane/portfolio.txt << 'EOF'
Client: Jane Smith
Risk Profile: Balanced
Reporting Date: 2026-03-05
Total Portfolio Value: $100,000

Holdings:
CBA: $50,000
VAS: $30,000
cash: $20,000

Asset Class Breakdown:
Australian Equities: 50%
International Equities: 0%
Fixed Income: 0%
Cash: 20%
Property / Infrastructure: 0%
Alternatives: 0%
EOF
```

## Step 3 — Confirm

Report back to the user:
- The full path to the created folder
- The contents of `portfolio.txt`
- Suggest the next command to run: `/portfolio-review ~/Documents/clients/smith-jane/portfolio.txt balanced`
