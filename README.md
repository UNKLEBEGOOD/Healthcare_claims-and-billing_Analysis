# Healthcare Claims & Billing Analysis

**Junior Data Analyst Portfolio Project**

**Author:** Odoh Ekenedirichukwu J.
**Background:** Registered Nurse (Ophthalmic Nursing) | Transitioning into Healthcare Data Analytics

---

## 📌 Project Overview

Healthcare organizations can lose significant revenue when insurance claims are denied or when the amount paid is lower than the amount billed.

In this project, I analyzed **70,000 healthcare billing records** covering **January to May 2025** to understand:

- How much of the billed amount was collected
- How much revenue remained unpaid
- Which insurance providers had higher denial rates
- The most common reasons for denied claims
- Whether claim denials were the main source of the revenue gap

The analysis was completed using **Python, SQL Server, and Power BI**.

---

## 📊 Power BI Dashboard Preview

<img src="https://raw.githubusercontent.com/UNKLEBEGOOD/Healthcare_claims-and-billing_Analysis/main/Health_billing_Portfolio/dashboard/healthcare_claim_billing_dashboard.png" alt="Healthcare Claims & Billing Dashboard" width="900">

**Dashboard file:** [Download the Power BI file (.pbix)](Health_billing_Portfolio/dashboard/healthcare_claim_billing_dashboard.pbix). Open it in Power BI Desktop to filter and explore.

---

## 🎯 Business Questions

1. **How much of the billed amount was actually collected?**
2. **Which insurance providers have the highest denial rates, and what are the common denial reasons?**
3. **Where is the biggest revenue gap coming from?**

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Python** | Data cleaning, exploration and analysis |
| **Pandas** | Data manipulation and calculations |
| **Matplotlib** | Data visualization |
| **Seaborn** | Exploratory data visualization |
| **SQL Server / T-SQL** | Data validation and analysis |
| **PyODBC / SQLAlchemy** | Connecting Python to SQL Server |
| **Power BI** | Interactive dashboard and reporting |
| **DAX** | KPI and calculated measures |
| **GitHub** | Project documentation and portfolio |

---

## 📊 Dataset

The dataset contains **70,000 billing records** from **January to May 2025**, with these fields:

- Billing ID, Patient ID, Encounter ID
- Insurance Provider, Payment Method
- Claim ID, Billing Date
- Billed Amount, Paid Amount
- Claim Status, Denial Reason

It covers **7 insurance providers**: Aetna, BCBS, Cigna, Humana, Medicaid, Medicare and UHC.

**Data folders:**
- [Raw data](Health_billing_Portfolio/data/raw)
- [Clean data](Health_billing_Portfolio/data/clean)

### Important Data Note

May 2025 is only a partial month, with records available up to **May 10**. The lower values shown for May should **not** be read as a full monthly decline in billing or payment activity.

---

## 🧹 Data Cleaning & Validation

Before the analysis, I ran several data quality checks:

- Missing values
- Duplicate records
- Negative billing and payment amounts
- Overpayments
- Missing claim IDs and missing denial reasons
- Claim status consistency
- Comparison of results between Python and SQL Server

### Missing Values

Not every missing value is a data quality problem.

- **Self-pay records do not have insurance claim IDs**, so missing claim IDs for these records were expected.
- **Denial reasons only apply to denied claims**, so paid claims with no denial reason were expected.

This helped me avoid removing valid records during cleaning. It also means claim counts and the denial rate use **insurance claims only (59,638)**, not all 70,000 records.

---

## 📈 Key Results

| Metric | Result |
|---|---:|
| Total Records | **70,000** |
| Insurance Claims | **59,638** |
| Total Billed | **$112.90M** |
| Total Paid | **$72.85M** |
| Revenue Gap | **$40.05M** |
| Collection Rate | **64.5%** |
| Denied Insurance Claims | **5,998** |
| Denial Rate | **10.1%** |

---

## 🔎 Key Findings

### 1. Only 64.5% of the billed amount was collected

The organization billed about **$112.90 million** and collected about **$72.85 million**, a revenue gap of about **$40.05 million**.

### 2. Denials were not the biggest source of the revenue gap

Denied claims accounted for about **$9.65 million** of the gap. About **$30.4 million (around 76%)** came from claims that were paid, but for less than the amount billed.

**Why this matters:** I first expected denials to be the main cause of lost revenue. Looking at the actual dollar amounts showed that **underpayments were a much larger issue**. This moved the focus from only reducing denials to also investigating reimbursement and payment differences.

---

## 🏥 Denial Rate by Insurance Provider

| Provider | Denial Rate |
|---|---:|
| Medicaid | **10.90%** |
| Cigna | **10.27%** |
| Humana | **9.99%** |
| UHC | **9.95%** |
| Medicare | **9.85%** |
| BCBS | **9.79%** |
| Aetna | **9.65%** |

Medicaid had the highest denial rate and Aetna the lowest. The gap between them is only about **1.25 percentage points**, so no single provider appears to drive the denial problem. This could point to broader claim submission or billing process issues, but more data would be needed to confirm that.

---

## ❌ Top Denial Reasons

| Denial Reason | Denied Claims |
|---|---:|
| Duplicate Claim | **472** |
| Prior Authorization Required | **457** |
| Service Not Covered | **437** |
| Timely Filing Limit Exceeded | **437** |
| Coordination of Benefits Issue | **436** |

There were **14 denial reasons** in total, and none dominated. Several of the most common ones could potentially be reduced through better claim tracking, eligibility verification, prior authorization processes, submission checks and timely claim submission.

---

## 💰 Collection Rate by Provider

Collection rates were similar across providers, from about **64.15% to 64.96%**. This suggests the revenue gap is not concentrated in one insurance provider but is more organization-wide.

---

## 🔍 Aetna: An Area for Further Investigation

Aetna had the **lowest denial rate** but also the **lowest collection rate** (64.15%, only slightly below Medicaid at 64.17%). A low denial rate does not automatically mean higher revenue collection. One possible explanation is differences in reimbursement rates or payment amounts, but this dataset does not have enough information to confirm the cause.

Further analysis could use contracted reimbursement rates, expected vs actual reimbursement, procedure-level payment rates and allowed amounts.

---

## 📊 Power BI Dashboard

I built an interactive **Power BI dashboard** to explore the claims and billing data.

**KPI cards:** Total Billed, Total Paid, Collection Rate, Denial Rate, Revenue Gap

**Visuals:**
- Monthly Billed vs Paid
- Denial Rate by Insurance Provider
- Claims by Status
- Denied Claims by Reason

**Filters (slicers):** Insurance Provider, Payment Method, Claim Status, Billing Quarter

The sidebar explains the metrics, and a Key Findings panel summarizes the main results.

### DAX Example

```dax
Total Claims =
CALCULATE(
    DISTINCTCOUNT(claims_and_billing_clean[claim_id]),
    claims_and_billing_clean[payment_method] <> "Selfpay"
)
```

Self-pay rows are excluded because they do not have a claim ID.

---

## 🧮 Python & SQL Validation

**Python (pandas)** was used for data cleaning, exploratory analysis, missing-value checks, aggregations, KPI calculations and visualizations.

**SQL Server (T-SQL)** was used to query the data, calculate key metrics, group claims by provider and denial reason, and cross-check the Python results.

The key calculations from Python and SQL Server **matched**, which gave me more confidence in the results.

---

## 📌 Recommendations

1. **Investigate underpayments first.** About 76% of the revenue gap came from paid claims that were reimbursed below the billed amount. Questions to ask: which procedures and providers have the largest payment differences, and are contracted reimbursement rates being applied correctly?
2. **Monitor Medicaid and Cigna.** They had the highest denial rates, though the differences between providers are small.
3. **Reduce preventable denials.** Focus on duplicate claims, prior authorization, service coverage, timely filing and coordination of benefits.
4. **Investigate Aetna reimbursement.** Its low denial rate combined with a low collection rate is worth a closer look.
5. **Monitor performance over time.** Use the dashboard to track collection rate, denial rate, revenue gap, provider performance and denial reasons each month.
6. **Treat May as preliminary.** The data stops on May 10, so May should not be compared directly with full months.

---

## 📁 Project Structure

```
Healthcare_claims-and-billing_Analysis/
│
├── README.md
└── Health_billing_Portfolio/
    ├── dashboard/
    │   ├── healthcare_claim_billing_dashboard.pbix
    │   └── healthcare_claim_billing_dashboard.png
    ├── data/
    │   ├── raw/
    │   └── clean/
    ├── notebooks/
    ├── reports/
    └── visuals/
```

### Project Files

| File / Folder | Description |
|---|---|
| [`dashboard`](Health_billing_Portfolio/dashboard) | Power BI file and dashboard screenshot |
| [`data/raw`](Health_billing_Portfolio/data/raw) | Original dataset |
| [`data/clean`](Health_billing_Portfolio/data/clean) | Cleaned dataset used for analysis and Power BI |
| [`notebooks`](Health_billing_Portfolio/notebooks) | Python and SQL analysis notebooks |
| [`reports`](Health_billing_Portfolio/reports) | Project reports |
| [`visuals`](Health_billing_Portfolio/visuals) | Exported charts |
| [Power BI file](Health_billing_Portfolio/dashboard/healthcare_claim_billing_dashboard.pbix) | Interactive dashboard |
| [Dashboard screenshot](Health_billing_Portfolio/dashboard/healthcare_claim_billing_dashboard.png) | Dashboard preview image |

---

## 📚 What I Learned

**Technical skills:** data cleaning with pandas, exploratory data analysis, SQL querying with SQL Server, connecting Python to SQL Server, KPI calculation, data visualization, Power BI dashboard development, DAX measures and cross-checking results between
