# Harshit Finance Analytics Lab — Excel-First Version

## What changed
This version removes public-company/private-company search completely.

The workflow is now:

1. Upload your Excel/CSV.
2. Normalize financial statement line items.
3. Validate available inputs.
4. Calculate financial ratios.
5. Run valuation.
6. Run credit analysis.
7. Generate a forecast.
8. Export normalized and analysis CSVs.
9. Print/save the result as PDF.

## Recommended Excel structure

Use the first row as headers:

| Metric | FY2024 | FY2025 | FY2026 |
|---|---:|---:|---:|
| Revenue | 1000 | 1180 | 1390 |
| Other Income | 20 | 24 | 28 |
| COGS | 600 | 690 | 800 |
| EBITDA | 210 | 250 | 300 |
| Depreciation | 55 | 60 | 65 |
| EBIT | 155 | 190 | 235 |
| Interest | 35 | 34 | 32 |
| PBT | 120 | 156 | 203 |
| Tax | 30 | 39 | 51 |
| PAT | 90 | 117 | 152 |
| Cash | 90 | 110 | 145 |
| Receivables | 150 | 175 | 205 |
| Inventory | 180 | 195 | 225 |
| Current Assets | 470 | 535 | 620 |
| Current Liabilities | 350 | 365 | 390 |
| Total Assets | 1500 | 1650 | 1840 |
| Equity | 600 | 690 | 805 |
| Borrowings | 500 | 480 | 450 |
| Net Debt | 410 | 370 | 305 |
| PPE | 700 | 770 | 840 |
| Intangibles | 80 | 85 | 90 |
| Retained Earnings | 250 | 320 | 435 |
| CFO | 150 | 175 | 220 |
| CFI | -100 | -120 | -130 |
| CFF | -40 | -35 | -55 |
| Capex | 100 | 120 | 130 |
| Working Capital | 120 | 170 | 230 |

## Important accuracy rule

The engine does NOT treat missing values as zero.

A ratio is calculated only when the required inputs exist and the denominator is non-zero.

The current DCF is intentionally labelled as a simplified starter model. Before using it for serious analysis, extend it to a full forecast with explicit Revenue, EBITDA margin, D&A, Capex, NWC, tax, WACC and terminal-growth assumptions for each forecast year.

## XLSX support

The HTML includes a parser hook for SheetJS. To make XLSX parsing work in a browser, load SheetJS before the main script and change the XLSX branch in `handleFile()` to call:

const buf = await file.arrayBuffer();
APP.rawRows = parseExcelWorkbook(buf);
buildModelFromRows(APP.rawRows);

For a production website, use a backend parser instead of exposing or trusting arbitrary client-side files.

## Where to edit

Search in `index.html` for these headings:

- `FILE UPLOAD`
- `SAMPLE DATA`
- `NORMALIZATION`
- `VALIDATION ENGINE`
- `DERIVED METRICS`
- `RENDER ENGINE`
- `CALCULATOR`
- `EXCEL PARSER HOOK`

The mapping dictionary is `ALIASES`.

If your Excel calls Revenue "Operating Revenue", add it to:

Revenue:["revenue","sales","net sales","turnover","total revenue","operating revenue"]

Do the same for any other line item.

## Next production upgrade

The best next step is to convert this standalone file into a full application with:

Frontend: Next.js + Tailwind
Backend: FastAPI or Node API
Excel parser: Python openpyxl/pandas
Database: PostgreSQL/Supabase
File storage: private object storage
Report generation: PDF + XLSX
Power BI: star-schema export
Authentication: private workspace/login
Audit trail: source file + mapping + calculation version
