# EverDriven Client Health Scoring Framework

A client health scoring system that turns service, client-experience and revenue data into a single 0–100 score for each school district account. For every metric below target, it recommends what the account team should do next.

> **Note:** This repository is a portfolio rebuild using **synthetic data**. Client names, account owners and all figures shown in the report are fictional. The results described under *Impact* come from the original framework in production at EverDriven.

**Links to Published Power BI Report**: 
- **GitHub**: https://thomasng303.github.io/ThomasN_Portfolio/everdriven/
- **Web Published**: https://app.powerbi.com/view?r=eyJrIjoiOWY3Mzg0ODQtMzY0YS00ZTViLWJkNDQtNmE0NjMyODZjNWNkIiwidCI6IjU2MzMzN2NhLWE1MTctNDIxYS1hYWUwLTFhYTViNDE0ZmQ3ZiIsImMiOjZ9

---

## Background

EverDriven provides alternative student transportation for school districts. It serves students with disabilities and others who can't ride a standard school bus, through a network of third-party service providers (TSPs). The company's revenue depends on districts renewing their contracts each year.

Before this framework, account health was judged account by account:

- Service, client and revenue data lived in **separate systems**, and pulling it together depended on **nine manual Excel reports**.
- There was **no consistent definition** of a "healthy" or "at-risk" account across area managers.
- Problems often came to light **during renewal conversations**, when it was too late to fix them.

The goal was one repeatable score covering roughly **600 legacy accounts** (clients with EverDriven for 2+ years). It needed to flag risk early and tell area managers exactly where to act.

---

## Data Sources

| Source | What it provided |
|---|---|
| **Salesforce** | Account records, account ownership, client interactions |
| **Published Power BI semantic model** (linked to the in-house routing and dispatch system) | On-time performance, complaints, driver rescues, trip volume |
| **Finance and billing records** | Revenue by fiscal year and year-over-year net revenue retention (NRR) |
| **Nine manual Excel reports** | Client experience scores and supplementary operational data, consolidated into the pipeline |

Fiscal years run July–June. Each year is compared over the same year-to-date window, so years are compared like for like.

---

## How the Score Works

### 1. Six metrics in three weighted categories

| Category | Weight | Metrics (equal weight within category) |
|---|---|---|
| **Revenue Retention** | 45% | YoY NRR |
| **Client Experience** | 30% | Client Experience Score, Client Interactions |
| **Service Quality** | 25% | On-Time %, Trips without Complaints, Trips without Rescues |

Revenue Retention carries the most weight because renewal is the outcome the business ultimately cares about. Service and experience metrics act as early warning signals.

### 2. Each metric is converted to a common 0–100 scale

| Metric | 0 | 25 | 50 | 75 | 100 |
|---|---|---|---|---|---|
| On-Time % | < 85% | 85–90% | 90–92% | 92–95% | ≥ 95% |
| Trips without Complaints | < 90% | 90–93% | 93–95% | 95–97% | ≥ 97% |
| Trips without Rescues | < 90% | 90–93% | 93–95% | 95–97% | ≥ 97% |
| Client Experience Score | < 90% | 90–93% | 93–95% | 95–97% | ≥ 97% |
| Client Interactions (per FY) | 0 | 1 | 2–3 | 4–5 | ≥ 6 |
| YoY NRR | < 75% | 75–90% | 90–100% | 100–110% | ≥ 110% |

A score of **75 is the ops target**, the threshold agreed in the operations meeting. Any metric scoring below 75 generates a prescription.

### 3. Health Score and status

The six metric scores are combined using the category weights into a **Health Score from 0 to 100**:

| Status | Health Score |
|---|---|
| **Healthy** | 70 and above |
| **Watch** | 45–69 |
| **At Risk** | below 45 |

### 4. Prescriptions

Each metric below target maps to a recommended action and the gap to close. For example:

| Metric below target | Recommended action |
|---|---|
| On-Time % | Work with the TSP on route-level on-time data; fix the most frequently late routes and tighten pickup windows |
| Trips without Rescues | Work with the TSP on driver attendance; assign backup drivers to the routes that need rescues most often |
| Client Interactions | Move to at least a quarterly business review with the district's transportation lead |
| YoY NRR | Review what drove the revenue change and address renewal risk before the next contract cycle |

---

## Validation

Before rollout, the framework was **back-tested on historical data**. Accounts were scored using a prior fiscal year's data, and the scores were compared against which clients actually **churned or chose not to renew** in the following year. The test confirmed that lower scores consistently flagged the accounts most likely to leave, so the score could be trusted as an early warning signal rather than a descriptive report card.

---

## Impact

- **Retention rose 5 percentage points year over year** after the framework was adopted.
- Area managers could **target outreach directly at flagged accounts**, leading each conversation with the specific metric driving the risk, instead of spreading attention evenly across their book.
- Nine manual Excel reports were replaced by a **single, consistent score** that every area manager and leader reads the same way.

---

## Report Walkthrough

### Client Health Command Center
- **KPI cards:** total legacy accounts, average Health Score, and how many accounts are Healthy, Watch and At Risk
- **Client Relationship Health Score:** every account with its score and color-coded status
- **Health Prescriptions:** every metric below target, with the gap to close and the recommended action
- **Top Issues Across the Portfolio:** how many accounts miss target on each metric
- **Health Breakdown by Area Manager:** each manager's accounts split into Healthy, Watch and At Risk
- **Filters:** by account and by area manager

### Account Deep Dive (drill-through)
Right-click any account on the Command Center and choose **Drill through → Account Deep Dive**.
- **Header:** account, area manager, Health Score and status
- **Metric cards:** all six metrics, colored green or red against target
- **Performance vs Ops Targets:** each metric as a % of its target
- **Revenue Trend FY24 → FY26:** a revenue bridge showing each year's growth or decline, ending at current FY26 revenue
- **Where the Points Come From:** points earned vs. missed in each category
- **Recommended Next Steps:** the account's prescriptions

### Resources
The scoring methodology, conversion scale, targets, weights and a guide to every chart.

---

## Technical Implementation

### Original (production at EverDriven)
- **Microsoft Fabric:** Lakehouse and Delta tables as the data foundation
- **Semantic Link (`sempy.fabric`)** for programmatic access to the published semantic model, which removed manual Power BI export workflows
- **Power BI on Direct Lake** for the reporting layer

### Portfolio rebuild (this repository)
- **Power BI Desktop / Service** in Import mode
- **Power Query (M):** source ingestion, metric-to-score conversion driven by a configurable band table, and calculation of the category and Health Scores, so each score is computed once at refresh
- **DAX:** rollups, status counts, gap-to-target and prescription logic, dynamic titles and labels, and conditional formatting
- **Drill-through** navigation from the portfolio view to account-level detail
- **Synthetic dataset** that mirrors the structure of the original data

---

## Data & Privacy

No EverDriven data is published in this repository. All accounts, owners and figures in the report are synthetic and do not represent real clients or real performance.
