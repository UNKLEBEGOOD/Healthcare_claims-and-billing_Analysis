# Healthcare Claims & Billing Analysis
### A Revenue Cycle & Claims Denial Case Study

**Author:** Odoh Ekenedirichukwu J.
**Background:** Registered Nurse (Ophthalmic Nursing) with 5+ years of clinical and EMR experience, transitioning into Healthcare Data Analytics.

---

## Business Problem

Healthcare providers routinely lose revenue to denied claims and underpayments from insurance payers. This project analyzes **70,000 billing records** across **7 insurance providers** (Aetna, BCBS, Cigna, Humana, Medicaid, Medicare, UHC) to quantify the size of the problem and pinpoint where the billing team should focus first.

**Questions answered:**
1. How much of billed revenue is actually being collected?
2. Which payers deny claims most often, and why?
3. Where is the biggest revenue gap, and what should be fixed first?

## Tools & Methods
- **Python** (pandas, matplotlib, seaborn) — data cleaning, exploratory analysis, visualization
- **SQL Server** (via pyodbc/SQLAlchemy, Windows Authentication) — key metrics reproduced and cross-validated with T-SQL
- **Power BI** — interactive dashboard built on the cleaned export (see `dashboard/power_bi_notes.md`)

## Data
70,000 rows spanning January-May 2025 (May is partial, only through the 10th), with billing ID, patient ID, encounter ID, insurance provider, payment method, claim ID, billing date, billed amount, paid amount, claim status (Paid/Denied), and denial reason. Missing `claim_id`/`claim_billing_date` were confirmed to belong only to Self-pay encounters (no insurance claim exists), and missing `denial_reason` belonged only to Paid claims — both expected, not data errors. No duplicates, negative amounts, or overpayments were found.

## Key Findings

| Metric | Value |
|---|---|
| Total Billed | $112,900,639.84 |
| Total Paid | $72,845,650.54 |
| **Revenue Gap (Billed - Paid)** | **$40,054,989.30** |
| Overall Collection Rate | **64.5%** |
| Denial Rate (insurance claims only) | **10.1%** |

**Denials by payer** — Medicaid has the highest denial rate (10.90%), followed by Cigna (10.27%); Aetna is lowest (9.65%). The spread across all 7 payers is narrow (~1.25 points), suggesting denials are driven more by **internal submission process issues** than by any single payer being unusually difficult.

**Top denial reasons:** Duplicate Claim (472), Prior Authorization Required (457), Service Not Covered / Timely Filing Limit Exceeded (437 each), and Coordination of Benefits Issue (436). All five are preventable through better front-end processes — claim tracking, eligibility verification, and timely submission — rather than payer negotiation.

**Collection rate by payer** is also tightly clustered (64.15%-64.96%), confirming the ~35% revenue gap is a **structural, organization-wide issue**, not isolated to one payer relationship. Notably, **Aetna has the lowest denial rate but also the lowest collection rate** — suggesting a separate issue (likely reimbursement rates) distinct from denials.

**Cross-validation:** All key metrics were independently reproduced using both pandas and SQL Server (T-SQL) queries, confirming consistent results across tools.

## Recommendations
1. **Target Medicaid and Cigna first** for a root-cause review of claim submission, though the narrow spread across payers suggests internal process fixes will help broadly.
2. **Fix the top 5 denial reasons** through staff training and pre-submission checklists — these are preventable, not payer-driven.
3. **Track denial rate and collection rate monthly** as standing KPIs using the Power BI dashboard, to measure whether process changes are working.
4. **Investigate Aetna's fee schedule specifically** — its low collection rate despite a low denial rate points to a reimbursement-rate issue, not a submission-process issue.
5. **Treat May figures as preliminary** — the dataset's most recent month is incomplete (only through the 10th), so recent-month trends should be confirmed once full data is available.

## Files in This Project
- `notebooks/claims_billing_analysis.ipynb` — full analysis: Python (pandas) + SQL Server (T-SQL), cross-validated
- `data/clean/claims_and_billing_clean.csv` — cleaned dataset (feeds Power BI)
- `visuals/` — all exported charts (PNG)
- `dashboard/power_bi_notes.md` — how to build the Power BI dashboard from the clean data


## Power BI Dashboard

![Dashboard Screenshot](../dashboard/dashboard_screenshot.png)

The full interactive file (`claims_billing_dashboard.pbix`) is available in the `dashboard/` folder — open with Power BI Desktop to filter and explore.
