# Online Retail Analysis with pandas

## Overview

A self-learning project practising the core pandas workflow on real-world transaction data: loading, cleaning, feature engineering, grouping, aggregation and RFM customer segmentation. The results are exported as CSV files for a follow-up visualisation project.

## Dataset

- **Source:** [E-Commerce Data on Kaggle](https://www.kaggle.com/datasets/carrie1/ecommerce-data), originally the UCI "Online Retail" dataset
- **Content:** all transactions of a UK-based online gift retailer between 1 December 2010 and 9 December 2011; many customers are wholesalers
- **Size:** 541,909 rows × 8 columns
- **Columns:** `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, `Country`

The raw data is not included in this repository. To run the notebook, download `data.csv` from Kaggle and place it in a `data/` folder in the project root.

## Workflow

1. **Data loading:** read the CSV with `encoding='latin-1'` and inspected structure and missing values.
2. **Type conversion:** converted `InvoiceDate` to datetime and `CustomerID` to string.
3. **Duplicates:** removed 5,268 duplicate rows.
4. **Cancellations:** separated orders with invoice numbers starting with `C` into a returns table.
5. **Invalid values:** removed rows with non-positive quantity or price, which were mostly internal stock adjustments without a customer ID.
6. **Missing customer IDs:** filled with a placeholder so these rows stay in revenue analysis but are excluded from customer-level analysis.
7. **Text cleaning:** stripped whitespace and uppercased product descriptions.
8. **Feature engineering:** added `TotalPrice` and extracted year, month, day, weekday, hour and year-month from the invoice date.
9. **Time series:** set the invoice date as the index, sliced by date, and resampled revenue by day, week and month.
10. **Aggregation:** summarised orders, customers and revenue by country; ranked top orders; analysed activity by weekday and hour; calculated average order value and month-over-month growth.
11. **Pivot table:** built a month × country revenue table.
12. **Transform:** calculated each line item's share of its order total.
13. **Return rates:** merged sales and cancellations by product to calculate return rates.
14. **RFM analysis:** calculated Recency, Frequency and Monetary values for each customer, scored them 1–5 with `pd.qcut()`, and combined them into an RFM score.
15. **Export:** saved summary tables to the `outputs/` folder.

## Tools

Python, pandas, NumPy, Jupyter Notebook

## Next Steps

Use the exported CSV files in `outputs/` to build visualisations, including monthly revenue trends, country comparisons and the distribution of customer RFM scores.
