# IKEA Customer Analytics: RFM Segmentation and Churn Analysis

In this project I took a large set of retail transactions, cleaned it in SQL Server, grouped customers using RFM analysis in Python, and built a Power BI dashboard to see who the best customers are and who is likely to leave.

"IKEA" here is just a made-up brand name for a practice project. It has nothing to do with the real IKEA company, and all numbers come from a public dataset.

## What I wanted to find out

- Who are the most valuable customers and how much revenue do they bring in?
- Which customers have stopped buying and may be lost?
- How do revenue and churn change across months, quarters and years?
- How do customers differ from country to country?

## Dataset

I used the Online Retail II dataset from the UCI Machine Learning Repository (donated by Daqing Chen). It has real, anonymized transactions of a UK online gift shop from December 2009 to December 2011 and is licensed under CC BY 4.0.

## Tools

- SQL Server for cleaning the data
- Python (pandas) in Jupyter Notebook for the RFM analysis
- Power BI for the dashboard

## How I did it

**1. Cleaning in SQL Server.** I combined the raw sheets into one table and checked that the dates and prices converted properly. Then I looked for missing customer IDs, zero or negative quantities, missing descriptions and exact duplicate rows. I removed the duplicates using ROW_NUMBER() and saved the result as a cleaned table with 1,033,036 rows. I exported it as RetailCleaned.csv.

**2. RFM analysis in Python.** I kept only rows with a customer ID and a positive quantity. For every customer I calculated:

- Recency: days since the last purchase (counted from one day after the last invoice date in the data)
- Frequency: number of unique invoices
- Monetary: total amount spent

Each one was scored from 1 to 5 using quintiles, and customers were put into six segments:

| Segment | Rule |
|---|---|
| Champions | R, F and M all 4 or above |
| Loyal | R 3 or above and F 3 or above |
| At Risk | R 2 or below and F 3 or above |
| New | R 4 or above and F 2 or below |
| Needs Attention | R 2 or below and F 2 or below |
| Lost | everyone else |

I treated a customer as churned if they had not purchased in the last 90 days. The scores and segments were then merged back with the transactions and saved as an Excel file for Power BI.

**3. Dashboard in Power BI.** The report has three pages:

- Home page with links to the other pages and a short glossary of the metrics
- Business Overview with total customers, revenue, churn % and average customer value, plus revenue by segment, month, quarter and year
- RFM Analysis with a segment summary table, average customer value by segment and churn trends over time, with a switch between Segment and Country

You can filter by month, quarter, year, country, segment and churn status. A PDF export of the dashboard is in this repo.

## What I found

- There are 5,881 customers and total revenue is $17.4M. Overall churn is 50.86% and the average customer value is 2,954.
- Champions are around 22% of customers but bring in about 68% of the revenue ($11.8M).
- A Champion is worth 9,169 on average, compared to 429 for a Lost customer.
- Loyal ($2.7M) and At Risk ($1.6M) customers are the next biggest revenue groups, so they are the ones worth keeping.
- Revenue is highest in Q4 ($6.2M) and November is the best month ($2.32M).
- Churn was highest in 2010 (56.30%) and lowest in 2011 (31.52%).

## Files in this repo

- `IKEA RFM Segmentation.ipynb`: the RFM analysis notebook
- `EcommerceDashboardData.xlsx`: the final data used in Power BI
- `IKEA_Customer_Analytics_Dashboard.pdf`: PDF of the dashboard
- `IKEA Project Theme.json`: Power BI theme file
- `Images.zip`: images used in the dashboard design

RetailCleaned.csv is not uploaded because it is over 100 MB, which is more than GitHub allows. The notebook reads this file, so to run it again you need to recreate it from the Online Retail II data using the cleaning steps above.

## Contact

- GitHub: https://github.com/sanjeetdwivedi21
- LinkedIn: www.linkedin.com/in/sanjeet-dwivedi-854539434

## Credits

The project idea and dashboard design are by Mansi Goel (Mansi G.): [github.com/the-mansi-goel/IKEA](https://github.com/the-mansi-goel/IKEA). I rebuilt the project myself, from data cleaning to the dashboard.
