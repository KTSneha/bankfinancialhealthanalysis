# Indian Banking Sector — Financial Health Analysis

## Overview
A financial-analyst-style comparative study of 5 major Indian banks (SBI, HDFC Bank, 
ICICI Bank, Kotak Mahindra Bank, Axis Bank) across FY2023–FY2026, using real 
financial statement and stock data pulled via `yfinance`. The project computes 
bank-specific financial ratios, builds a composite Financial Health Score, and 
verifies unusual trends against real corporate events (mergers/acquisitions).

## Why bank-specific ratios?
Banks don't report financials like typical companies — there's no "Current Assets" 
or generic "Operating Income" line, because their core business (loans, deposits, 
interest) doesn't fit that structure. This project uses ratios standard to bank 
analysis instead:

| Ratio | Formula | What it measures |
|---|---|---|
| ROE | Net Income / Stockholders Equity | Shareholder profitability |
| ROA | Net Income / Total Assets | Asset-efficiency profitability |
| NIM | Net Interest Income / Total Assets | Core lending margin |
| Equity-to-Assets | Stockholders Equity / Total Assets | Capital cushion / stability |
| Cost-to-Income | Operating Expense / Total Revenue | Operating efficiency (lower = better) |

## Data caveat: Cost-to-Income
HDFC Bank and ICICI Bank's filings don't report a single "Operating Expense" line; 
Selling, General & Administrative (SG&A) expense is used as a proxy instead. This 
likely **understates** their true cost base relative to SBI/Kotak/Axis, which report 
operating expense directly. Cross-bank Cost-to-Income comparisons should be read with 
this in mind; within-bank trends over time remain valid. The composite Health Score 
excludes this metric's bias by scoring HDFC/ICICI neutrally on this component rather 
than let the reporting gap distort the ranking.

## Composite Financial Health Score
A weighted, peer-relative (min-max normalized) score per year:
- ROE (25%), ROA (25%), NIM (20%), Equity-to-Assets (15%), Cost-to-Income (15%, 
  reported-basis banks only)
- Normalized **within each year** separately, so scores reflect standing relative 
  to peers at that point in time, not distorted by universal asset growth over years.
- Scores are relative to this 5-bank peer set, not an absolute industry benchmark.

## Key findings
- **ICICI Bank and Kotak Mahindra Bank** lead the peer set across most years on 
  profitability and margin metrics.
- **SBI** is structurally at the bottom of this peer set across all 4 years — 
  consistent with a large, PSU-scale balance sheet rather than year-over-year decline.
- **HDFC Bank's Health Score drops sharply from FY23 to FY24** — this coincides with 
  its merger with HDFC Ltd (effective July 1, 2023), which expanded its equity base 
  significantly and diluted ROE/ROA in the near term.
- **Axis Bank's lowest score is FY23**, coinciding with one-time acquisition costs 
  from its Citibank India consumer business acquisition (completed March 1, 2023), 
  recovering sharply the following year.

## Tools used
Python, pandas, yfinance, matplotlib

## Limitations
- Min-max normalization with only 5 banks is sensitive to outliers — each year's 
  scale is anchored by whichever bank is highest/lowest that year.
- Cost-to-Income basis inconsistency (see caveat above).
- 4 fiscal years is a relatively short window for trend analysis.