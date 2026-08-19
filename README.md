# Customer Churn Analysis & Retention Insights

Exploratory analysis of subscription churn drivers using customer, subscription/billing, and support-interaction data, done end-to-end in Python/pandas with a SQLite staging layer.

## Problem
A subscription business wants to know which customer segments and behaviors are driving cancellations, so retention spend can be targeted instead of spread evenly.

## Data
Three tables (originally an Excel export, staged into SQLite for querying):
- **db_customer** — demographics (country, state, gender, interests)
- **db_subscription** — plan type, contract type, billing, CLTV, cancellation details, and a pre-computed `churn_score`
- **db_support** — support tickets, escalation flags, CSAT scores

## Approach
1. Loaded raw Excel sheets into a local SQLite DB, queried back into pandas
2. Cleaned inconsistent categorical labels (gender, missing country), cast date columns, dropped an empty column
3. Defined churn as presence of a cancellation date
4. Compared churn rate across plan type, contract type, support escalation history
5. Validated the provided `churn_score` against actual churn outcomes
6. Quantified revenue/CLTV impact of churned vs retained customers

## Key findings
- **Contract type is the strongest churn driver**: monthly contracts churn at 56% vs 8% for annual contracts
- **Basic-plan customers churn at 60%**, ~4x the Premium rate — driven mainly by "not enough content" as a stated cancellation reason, not price
- **`churn_score` is a usable early-warning signal** — correlates at r ≈ 0.86 with actual churn
- **Support escalations are a near-certain churn precursor** in this sample, and should trigger a retention follow-up, not just ticket resolution

Full analysis, charts, and recommendations are in [`churn_analysis.ipynb`](./churn_analysis.ipynb).

## Tools
Python, pandas, SQLite, matplotlib, seaborn

## Limitations
Small sample (21 customers) — findings are directional and would need validation on a larger extract before driving actual retention spend. Noted as a next step in the notebook.

## Author
Rahul Kumar
