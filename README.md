# UK-Online-Retail-ETL-Customer-Analysis

A full ETL and exploratory analysis project on the UK Online Retail dataset (Kaggle), covering data cleaning, feature engineering, customer segmentation (RFM), and revenue analysis.

The dataset was downloaded from here: https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci

## Tools
Python, pandas, matplotlib, Jupyter Notebook

## What I Did

**Extract**
- Loaded ~1M+ rows of UK e-commerce transaction data (2009–2011)

**Transform**
- Converted `InvoiceDate` to proper datetime (to extract month and year later)
- Identified and removed exact duplicate rows (verified by sorting and manually inspecting matched pairs before dropping)
- Handled missing `Customer ID` and `Description` values by labeling them `'Unknown'` rather than dropping 25% of the rows with missing Customer ID. This helped preserve transaction-level data (revenue, product volume) while still enabling customer-level analysis to exclude them where appropriate
- Identified and separated cancelled transactions (Invoice numbers starting with 'C') from genuine sales
- Engineered `TotalPrice` (Quantity × Price) and `YearMonth` for time-based analysis

**Analyze**
- Top 10 customers and top countries by revenue
- Monthly revenue trend
- Customer segmentation: Known vs. Unknown purchase behavior
- RFM (Recency, Frequency, Monetary) segmentation into Champions, Loyal Customers, Potential Loyalists, At Risk, and Lost customers

## Key Insights

1. **25% of transactions have no CustomerID.** Dropping these rows would have understated total revenue and introduced bias — they were labeled `'Unknown'` instead, preserving transaction-level accuracy while keeping customer-level metrics (like RFM) clean.

2. **Known customers buy in bulk** (~12.6 units/transaction) at a lower unit price (£3.70); Unknown/guest transactions are small, single-item purchases (~1.5 units) at a higher unit price (£7.71). This suggests "Known" customers are largely repeat/wholesale business accounts, while "Unknown" transactions represent individual consumers.

3. **RFM segmentation** reveals 22% of customers are "Champions", while 24% are "Loyal Customers", 14% are "Potential Loyalists", and 26% fall into "At Risk" or "Lost" = a clear target for re-engagement.

4. Top-country and monthly-trend findings: 
<img width="863" height="515" alt="image" src="https://github.com/user-attachments/assets/6e294235-8ac7-4904-b2e6-86a038b55342" />
<img width="873" height="517" alt="image" src="https://github.com/user-attachments/assets/c43a4264-9726-40a1-934b-a84690010181" />
<img width="1121" height="523" alt="image" src="https://github.com/user-attachments/assets/2cee8394-1653-447a-8d9c-36e88aebbfad" />

## Notes
All cleaning decisions (drop vs. fill, include vs. exclude cancellations) were made deliberately based on what each downstream analysis required, not applied as blanket defaults.

The Jupyter Notebook: https://github.com/AnnieQurat/UK-Online-Retail-ETL-Customer-Analysis/blob/main/Online_Retail_II.ipynb
