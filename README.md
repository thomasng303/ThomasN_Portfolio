# Thomas Nguyen — Analytics Portfolio

BI Analyst and junior data scientist working across Power BI, Microsoft Fabric, and Python. The projects below are rebuilt from real work engagements using anonymized and synthetic data.

---

## 1. Client Health Scoring Framework (EverDriven)

**Reporting Tools:** Power BI · DAX · Power Query · Python (pandas and SciPy (weight optimization using constraints optimization techniques)
**Data Integration Tools (Microsoft Fabric)**: Copy Job ingestion, PySpark Fabric Notebooks for complex transformations and data operations, Pipeline orchestration to move and deliver gold tables for reporting needs.

### Links to Published Power BI Report
**GitHub**: https://thomasng303.github.io/ThomasN_Portfolio/everdriven/
**Web Published**: https://app.powerbi.com/view?r=eyJrIjoiOWY3Mzg0ODQtMzY0YS00ZTViLWJkNDQtNmE0NjMyODZjNWNkIiwidCI6IjU2MzMzN2NhLWE1MTctNDIxYS1hYWUwLTFhYTViNDE0ZmQ3ZiIsImMiOjZ9

### Background
EverDriven provides alternative student transportation for school districts, serving students with disabilities and others who can't ride a standard school bus, through a network of third-party service providers. Account health was previously judged account by account, with no consistent way to tell which districts were at risk of leaving or what to do about it.

### Data sources
The original framework brought together data from across the business:
- **Salesforce:** account records and client interactions
- **A published Power BI semantic model** connected to the in-house routing and dispatch system, and Azure database: on-time performance, complaints and driver rescues, revenue and year-over-year net revenue retention
- **Nine manual Excel reports**, consolidated into a single automated pipeline

### What I built
A **Client Health Score (0–100)** for each of EverDriven's roughly **600 legacy accounts** (2+ years with the company). It combines six metrics across three weighted categories: Revenue Retention (45%), Client Experience (30%) and Service Quality (25%). Each metric is converted to a common 0–100 scale against ops-approved targets. The report has three pages:

- **Client Health Command Center:** portfolio KPIs, every account's score and status (Healthy / Watch / At Risk), the most common issues across the portfolio, and a health breakdown by area manager
- **Account Deep Dive (drill-through):** right-click any account to see its metrics against target, a revenue bridge from FY24 to FY26, where its score is losing points, and the recommended next steps
- **Resources:** the scoring methodology, targets and a guide to every chart

Every metric below target automatically generates a **prescription**: the gap to close and a concrete action, such as "work with the transportation provider on route-level on-time data".

### Validation
Before rollout, the score was back-tested on historical data. Accounts were scored using a prior fiscal year's data, then compared against which clients actually churned or chose not to renew the following year. This confirmed that lower scores reliably flagged the accounts most likely to leave.

### Outcome
-  **Retention rose 5 percentage points year over year** after the framework was adopted. Instead of spreading attention evenly across the book, area managers could target outreach directly at the accounts flagged At Risk or Watch, and lead each conversation with the specific metric driving the risk, whether late routes, driver no-shows, low engagement or shrinking revenue. Problems got addressed before the renewal conversation, rather than discovered during it.
- **30 at-risk accounts were saved** through targeted interventions guided by the prescriptions
- Area managers got one page per account to bring into client meetings, with clear, prioritized actions instead of raw metrics

### About this portfolio version
This repository is a rebuild using **synthetic data** that mirrors the structure of the original. It scores 367 synthetic legacy accounts, flagging 106 as At Risk and 81 for monitoring. In its own back-test, synthetic accounts flagged At Risk churned at 29% the following year, vs. 11% for Healthy accounts. These figures illustrate how the framework works and are not EverDriven's actual results.

---

## 2. EHS Exposure Analysis: LEL & H2S Events (Ovintiv)

**Tools:** Power BI · DAX · Power Query

### Background
Field crews in oil and gas operations can be exposed to two serious atmospheric hazards: combustible gas reaching its lower explosive limit (LEL) and hydrogen sulfide (H2S). Environmental, Health & Safety (EHS) teams record these exposure events, but the raw logs don't show where or why risk concentrates. This project turns those logs into a view of which operational activities and conditions drive exposure risk.

### What's in the report
- **Executive Summary:** overall exposure event volume, severity and trends at a glance
- **Risk by Operational Activity:** exposure risk broken down by the task being performed, so safety controls can target the riskiest work

### Outcome
EHS leaders get a single view that shows which activities and locations carry the highest exposure risk, so they can prioritize safety controls and equipment investments where they reduce the most risk. The original hotspot analysis of atmospheric hazard readings informed funded air vent upgrades.

---

### Data & privacy
No confidential company data is published. The Ovintiv project uses anonymized data, and the EverDriven project uses synthetic data with fictional client names and account owners.

### Contact
Thomas Nguyen · Denver, CO · thomas.hb.nguyen@gmail.com
