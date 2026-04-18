# cms-hospital-analyzer
U.S. Hospital Quality, Spending & Readmission analysis using the CMS API

**Status:** Analysis Phase  
**Author:** Fatima Zahra Boutkhil — Data Analyst in the Making  
**Data Source:** [CMS Hospital Compare](https://data.cms.gov/provider-data/) via public API

---

## What This Project Is About

The Centers for Medicare & Medicaid Services (CMS) sits right under HHS and is the on-the-ground force that manages the money and rules for U.S. hospitals. That makes it a uniquely rich source for understanding how the American healthcare system actually performs — not in theory, but in dollars, outcomes, and patient experience.

This project started as a broad exploration of hospital quality across the U.S. Through early analysis, one paradox kept surfacing:

> **A hospital can be measured very differently depending on whether you look at mortality rates versus safety rates. The best hospital on one dimension can be the worst on another.**

That led to a sharper, more focused question.

---

## Central Research Question

**Why is hospital spending not linearly related to clinical outcomes — and what explains the hospitals that spend more but achieve worse results?**

The hypothesis driving this analysis: some hospitals spend more *because* their processes fail — excess infections, avoidable readmissions, unnecessary visits — not because their patients are inherently sicker. In those cases, spending is a symptom of dysfunction, not an investment in quality.

---

## Analytical Framework

The analysis is structured in five layers, each building toward the central question:

**Layer 1 — Establish the paradox**  
Does higher spending actually produce better clinical outcomes? What share of hospitals are high-spend with poor outcomes vs. low-spend with good outcomes?

**Layer 2 — Profile the inefficient hospitals**  
Who are they? Do they cluster by state, ownership type (for-profit vs. non-profit vs. government), or hospital size?

**Layer 3 — Identify the process failures**  
Do high-spend hospitals have worse infection rates? Higher readmissions? More unplanned visits? Where is the money actually going?

**Layer 4 — The patient experience disconnect**  
Do patients in high-spending hospitals rate them higher? Or are those hospitals spending more and still delivering poor satisfaction?

**Layer 5 — Synthesize**  
What combination of factors best explains the spending-outcome gap? Can hospitals be grouped into meaningful archetypes based on their spending and quality profile?

---

## Data

Eight datasets pulled from the CMS public API, cleaned, and loaded into a local SQLite database (`cms_hospital.db`):

| Dataset | Description |
|---|---|
| `hospital_general_info` | Hospital type, ownership, location, star rating |
| `readmissions_and_deaths` | 20 readmission and mortality measures |
| `medicare_spending` | Per-episode spending by claim type and period |
| `healthcare_infections` | Standardized Infection Ratios (SIR) |
| `hcahps_patient_survey` | Patient experience and satisfaction scores |
| `unplanned_visits` | 14 measures of avoidable/unplanned hospital visits |
| `timely_effective_care` | 30 process-of-care and timeliness measures |
| `payment_and_value` | Payment and value-of-care measures |

---

## Project Structure

```
cms-hospital-analyzer/
├── Data/            ← raw CSVs (gitignored)
├── Notebooks/       ← ingestion and cleaning notebooks (01–11)
├── sql/             ← analysis notebooks (SQL_analysis_01 onward)
├── outputs/         ← exported tables and charts
├── src/             ← helper scripts
├── cms_hospital.db  ← final SQLite database (gitignored)
└── README.md
```

---

## Pipeline Summary

| Step | Notebook | Description |
|---|---|---|
| Ingestion | `01_data_ingestion` | Pulls 8 datasets via CMS API (paginated, limit=1500) |
| Surface cleaning | `02_data_cleaning` | Standardizes nulls, types, column names |
| Deep cleaning | `03` – `10` | One notebook per dataset — fixes, pivots to wide format |
| Database setup | `11_setup_database` | Loads all 8 tables into SQLite |
| Analysis | `sql/SQL_analysis_*` | SQL + pandas queries across all tables |

---

## Tools

- Python, Pandas, SQLite3
- Jupyter Lab
- CMS public API (no key required)
- GitHub Desktop