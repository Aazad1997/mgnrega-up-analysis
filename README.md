# mgnrega-up-analysis
SQL analysis of district-level rural employment scheme data (MGNREGA / VB-G RAM G) for Uttar Pradesh, FY 2024-25 onwards. Built with Postgres.
## Questions

### A. Delivery (current data)
1. Which districts have the largest gap between work demanded and work offered?
2. How did persondays and 100-day completions change from 2024-25 to 2025-26? (2026-27 is a partial year, so it's shown separately.)
3. Where are job cards being deleted at unusually high rates?

### B. Social composition (current data)
4. How does the SC/ST share of job cards relate to demand and to work delivered?

### C. Poverty and need (needs NITI Aayog MPI data, planned)
5. Do districts with higher multidimensional poverty have a higher share of job-card households demanding work?
6. Is work offered in proportion to demand in poorer districts?
7. Do poorer districts get more days of work per household and more 100-day completions?
8. How do richer or more urban districts (such as Ghaziabad and Gautam Buddha Nagar) compare?

### D. Payments (planned, needs report R8.1)
9. Where are payment delays longest, and do they relate to lower participation?

## Data
- Source: official government portals for the scheme, report R5.1.1
  (Employment Generated during the year), district-wise, Uttar Pradesh.
- Years: 2024-25, 2025-26, 2026-27 (partial year, still in progress).
- `data/raw/` holds the original downloads, unchanged.
- `data/up_r5_1_1_clean.csv` is the cleaned, combined file.

## Data cleaning
- Merged the two-row header into one row with consistent snake_case names
- Removed the state total rows (verified totals against the loaded table)
- Added a `fin_year` column and stacked the three files (75 districts x 3 years)
- Loaded into Postgres with a unique key on (fin_year, district)

## Limitations
- 2026-27 is a partial year, so I compare it using ratios, not raw totals.
- The scheme changed to VB-G RAM G in 2026-27, so definitions may differ.

## Tools
Excel / LibreOffice (cleaning), PostgreSQL + DBeaver (analysis), Docker.
