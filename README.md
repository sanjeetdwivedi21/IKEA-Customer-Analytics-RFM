# IKEA Customer Analytics: RFM Segmentation and Churn Analysis

An end-to-end data analytics project covering data cleaning in **SQL Server**, customer segmentation with **RFM analysis in Python**, and an interactive **Power BI** dashboard that turns raw transactions into retention insights.

## Disclaimer

"IKEA" is used only as a fictional brand name for an educational portfolio project. This project is not affiliated with, endorsed by or representative of the real IKEA corporation. All figures come from a public, anonymized transactional dataset and do not reflect any real company's performance.

## Business Problem

The business wants to identify its most valuable customers and reduce churn among customers who are at risk of leaving. Without a structured view of customer value, retention efforts stay reactive instead of targeted.

### Questions Answered

- Who are the most valuable customers, and how much revenue do they contribute?
- Which customers have gone quiet and are at risk of churning?
- How do customer value and retention trend by month, quarter and year?
- How do customer value and churn differ across countries?
- Which actions suit each customer segment?

## Data Source

**Online Retail II**, UCI Machine Learning Repository, donated by Daqing Chen. It contains real, anonymized transactions of a UK-based online gift retailer from December 2009 to December 2011, and is licensed under Creative Commons Attribution 4.0 International (CC BY 4.0).

## Tech Stack

| Stage | Tool |
|---|---|
| Data cleaning and validation | SQL Server (T-SQL) |
| RFM scoring and segmentation | Python (pandas), Jupyter Notebook |
| Visualization | Power BI |

## Project Workflow

1. **Data cleaning (SQL Server):** consolidated the raw sheets into one table with the source sheet retained, validated date and price conversions, and checked for missing customer IDs, non-positive quantities, missing descriptions and exact duplicates. Duplicates were removed with the `ROW_NUMBER()` window function, giving a cleaned table of **1,033,036 records** (`RetailCleaned.csv`).
2. **RFM analysis (Python):** calculated Recency, Frequency and Monetary values for each customer, scored them and assigned segments (see below), then flagged churned customers.
3. **Dashboard (Power BI):** merged the segmentation results back onto the transactions (`EcommerceDashboardData.xlsx`) and used it as the single source for the report.

## RFM Methodology

Only transactions with a valid customer ID and a positive quantity were used. The snapshot date is one day after the last invoice date.

| Metric | Definition |
|---|---|
| Recency | Days since the customer's last purchase |
| Frequency | Number of unique invoices |
| Monetary | Total spend (quantity x price) |

Each metric is scored from 1 to 5 using quintiles. Customers are then segmented as follows:

| Segment | Rule |
|---|---|
| Champions | R >= 4, F >= 4 and M >= 4 |
| Loyal | R >= 3 and F >= 3 |
| At Risk | R <= 2 and F >= 3 |
| New | R >= 4 and F <= 2 |
| Needs Attention | R <= 2 and F <= 2 |
| Lost | All remaining customers |

A customer is flagged as **churned** when Recency is more than 90 days.

## Dashboard

The report (`IKEA_Customer_Analytics_Dashboard.pdf`) has three pages:

- **Home:** navigation to the report pages and a glossary of Recency, Frequency, Monetary and Churned %.
- **Business Overview:** Total Customers, Total Revenue, Churned % and Average Customer Value, with a revenue/customer toggle, segment breakdowns and month, quarter and year trends. Filterable by month, quarter, year, country, segment and churn status.
- **RFM Analysis:** segment performance summary (customers, revenue, average R/F/M scores), average customer value by segment, and churn trends over time, with a Segment/Country toggle.

## Key Findings

- **5,881 customers** generated **$17.4M** in revenue, with an overall churn rate of **50.86%** and an average customer value of **2,954**.
- **Champions** are about 22% of customers but generate roughly **68% of revenue ($11.8M)**, a clear 80/20-style concentration.
- Average customer value varies sharply by segment: 9,169 for Champions against 429 for Lost customers.
- **Loyal ($2.7M)** and **At Risk ($1.6M)** customers are the main retention opportunity.
- Revenue peaks in **Q4 ($6.2M)**, with **November the strongest month ($2.32M)**, consistent with a gifting-focused product category.
- Churn was highest in **2010 (56.30%)** and lowest in **2011 (31.52%)**.

## Repository Contents

```
IKEA-Customer-Analytics-RFM/
├── README.md
├── .gitignore
├── IKEA RFM Segmentation.ipynb
├── RetailCleaned.csv
├── EcommerceDashboardData.xlsx
├── IKEA_Customer_Analytics_Dashboard.pdf
├── IKEA Project Theme.json
└── Images.zip
```

| File | Description |
|---|---|
| `IKEA RFM Segmentation.ipynb` | RFM calculation, scoring, segmentation and churn flagging |
| `RetailCleaned.csv` | Cleaned transactions exported from SQL Server (input to the notebook) |
| `EcommerceDashboardData.xlsx` | Transactions merged with RFM results (data source for Power BI) |
| `IKEA_Customer_Analytics_Dashboard.pdf` | Export of the three-page Power BI dashboard |
| `IKEA Project Theme.json` | Power BI report theme |
| `Images.zip` | Image assets used in the dashboard design |

## How to Run

1. Install the requirements: `pip install pandas openpyxl jupyter`
2. Open `IKEA RFM Segmentation.ipynb` with `RetailCleaned.csv` in the same folder and run all cells. This produces `EcommerceDashboardData.xlsx`.
3. In Power BI Desktop, load `EcommerceDashboardData.xlsx` and apply `IKEA Project Theme.json` (View > Themes > Browse for themes).

## Contact

- GitHub: [your-username](https://github.com/your-username)
- LinkedIn: [your-profile](https://www.linkedin.com/in/your-profile)

## Credits

The project concept and dashboard design are by **Mansi Goel (Mansi G.)**: [github.com/the-mansi-goel/IKEA](https://github.com/the-mansi-goel/IKEA). I rebuilt the project myself, from data cleaning through to the dashboard. Dataset: Daqing Chen, UCI Machine Learning Repository (CC BY 4.0).
