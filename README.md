# Provider Hours Analyzer

Internal tool for analyzing provider billing hours from Focus reports. Calculates weekly hours worked by each provider and identifies billing corrections.

## Quick Start

1. Open `provider-hours-analyzer.html` in any modern browser (Chrome, Edge, Firefox, Safari)
2. Click the **"Open Report in Focus"** button to access the data source
3. Export the Focus report as Excel (.xlsx)
4. Drag and drop the file onto the upload area (or click to browse)

## Data Source

**Focus Report:** Billing by Service Date Range  
[Direct Link](https://tis.focuscbmapp.com/reports/datageniereport?id=901d9d41-94a7-4ff9-9df0-5aede6a917dd&name=Billing%20by%20Service%20Date%20Range)

### Required Columns

| Column | Description |
|--------|-------------|
| FullName | Client/patient name (used for correction matching) |
| Begin Date | Service date (used to determine which week) |
| Total Units | Billing units (1 unit = 15 minutes) |
| Created By | Provider name |
| title | Record title (used to detect corrections) |

Optional columns for drill-down details: Begin Time, End Time, ProcCode, Funding Source

## Features

### Hours Analysis
- Calculates hours from units (15 min/unit)
- Groups by week (Sunday–Saturday)
- Shows total, average, max, and min weekly hours per provider
- Trend indicator comparing recent weeks

### Filtering & Sorting
- **Hours Threshold:** Filter to show only providers who worked ≥ X hours in at least one week
- **Date Range:** Analyze specific time periods
- **Search:** Find providers by name
- **Sort:** By max hours, total hours, avg hours, corrections, name, etc.

### Correction Tracking
Records are flagged as corrections if the `title` column contains the word "correction" (case-insensitive). The app tracks:
- Total correction hours per provider
- Correction hours per week
- Percentage of total hours that are corrections

**Affected Records:** When a correction exists for a specific client + date + provider combination, ALL records for that same combination are highlighted as "affected." This helps identify which service entries have been subject to billing corrections.

In the drill-down view:
- **Orange rows** = Actual correction records
- **Yellow rows** = Records affected by a correction (same client/date/provider as a correction)
- **No highlight** = Regular records with no related corrections

### Drill-Down
1. Click **View** on any provider to see their weekly breakdown
2. Click any week row to see all individual records for that week
3. Correction records are highlighted in orange

### Export
Click **Export Excel** to download a workbook with three sheets:
- **Provider Summary:** All providers with totals and stats
- **Weekly Breakdown:** Hours by provider by week
- **Statistics:** Report metadata and totals

## Notes

- All processing happens in your browser—no data is uploaded anywhere
- Works offline once the page is loaded
- Week definition: Sunday through Saturday
- The file resets when you close the browser; export your analysis if you need to save it

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Could not find required columns" | Make sure the Excel file has columns named "Begin Date", "Total Units", and "Created By" |
| Dates look wrong | Check that the Focus export has dates in M/D/YYYY format |
| Provider missing | They may be filtered out by the hours threshold—try setting it to 0 |

---

© 2025 Accelerate Solutions, LLC
