---
description: Gather market intelligence using web search and generate a structured daily report
---

# Generate Daily Market Intelligence Report

Gather macro news, market movers, and sector performance data, then generate and save a structured market report.

## Step 1: Gather Market Data

Use the **WebSearch** tool to run the following searches. Run all searches in parallel for efficiency.

| Category | Search Query |
|----------|--------------|
| Macro & Policy | `latest macroeconomic news US Europe policy announcements equity markets {{date}}` |
| US Market Movers | `top gainers losers US stock market previous trading day {{date}}` |
| European Market Movers | `top gainers losers European stock market previous trading day {{date}}` |
| US Market Performance | `US equity index S&P 500 Nasdaq Dow Jones sector performance {{date}}` |
| European Market Performance | `European equity index STOXX 600 FTSE 100 DAX sector performance {{date}}` |

Where `{{date}}` is today's date.

## Step 2: Generate the Report

Synthesize the search results into this report structure:

```markdown
# DAILY MARKET INTELLIGENCE REPORT
**Date:** {{YYYY-MM-DD}} {{HH:MM AM/PM}}

## 1. Macro & Policy News
- Key macroeconomic developments
- Major policy announcements
- Focus on U.S. and European equity impact

## 2. Largest Market Movers

### U.S. Markets
| Top Gainers | % Change | Top Losers | % Change |
|-------------|----------|------------|----------|
| ... | ... | ... | ... |

### European Markets
| Top Gainers | % Change | Top Losers | % Change |
|-------------|----------|------------|----------|
| ... | ... | ... | ... |

## 3. Market & Sector Performance

### U.S. Indices
- S&P 500: [value] ([change])
- Nasdaq: [value] ([change])
- Dow Jones: [value] ([change])

### U.S. Sectors
- **Top 3:** [sectors]
- **Bottom 3:** [sectors]

### European Indices
- STOXX 600: [value] ([change])
- FTSE 100: [value] ([change])
- DAX: [value] ([change])

### European Sectors
- **Top 3:** [sectors]
- **Bottom 3:** [sectors]

---
*Sources: [list sources with URLs]*
```

## Step 3: Save the Report

Save the report to: `reports/market_report_{{YYYY-MM-DD}}_{{HH-MM}}.md`

Create the `reports/` folder if it does not exist.

## Constraints

- **Recency:** Only include information from the last 12 hours
- **Accuracy:** Extract only factual, verifiable data from search results
- **Transparency:** Never fabricate data—state "data not available" if missing
- **Provenance:** Include source URLs for all data points
- **Tone:** Concise, factual, professional

## Output

After saving, confirm with:

```
Report saved to: reports/market_report_{{YYYY-MM-DD}}_{{HH-MM}}.md
```