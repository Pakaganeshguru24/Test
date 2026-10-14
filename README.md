# Banking Transaction Analysis – SQL & Power BI Project

This project analyzes banking transactions using SQL Server and Power BI.  
It includes data cleaning, data modeling, KPI creation, and a 2-page interactive dashboard.

## Project Overview

The project uses transaction data containing customer, product, branch, date, transaction type, amount, status, and channel information.

The main goal is to analyze:

- Total transaction amount
- Transaction count
- Transaction success and failure rate
- Loan disbursement and repayment
- Credit card purchases and payments
- Deposits and withdrawals
- Fee and interest income
- Customer, product, branch, and region performance

## Tools Used

- SQL Server
- SQL Server Management Studio (SSMS)
- Power BI Desktop
- DAX
- Power Query

## Project Workflow

1. Created database and tables in SQL Server
2. Generated sample banking transaction data
3. Added dirty data such as null values, duplicates, incorrect formats, and inconsistent text
4. Cleaned data using Power Query in Power BI
5. Created a combined transaction table using SQL joins
6. Created DAX measures for KPIs
7. Designed a 2-page Power BI dashboard

## SQL Tables

The project uses the following tables:

- `Fact_Transactions`
- `Dim_Customer`
- `Dim_Product`
- `Dim_Branch`
- `Dim_Date`
- `Combined_Transactions`

The `Combined_Transactions` table combines transaction data with customer, product, branch, and date details.

```sql
SELECT
    f.TransactionID,
    f.TransactionAmount,
    f.TransactionType,
    f.TransactionStatus,
    c.CustomerName,
    c.City,
    c.State,
    c.AccountType,
    c.CustomerSegment,
    p.ProductName,
    p.ProductCategory,
    b.BranchName,
    b.Region,
    d.FullDate,
    d.MonthName,
    d.Year
INTO dbo.Combined_Transactions
FROM dbo.Fact_Transactions AS f
INNER JOIN dbo.Dim_Customer AS c
    ON f.CustomerID = c.CustomerID
INNER JOIN dbo.Dim_Product AS p
    ON f.ProductID = p.ProductID
INNER JOIN dbo.Dim_Branch AS b
    ON f.BranchID = b.BranchID
INNER JOIN dbo.Dim_Date AS d
    ON f.DateKey = d.DateKey;
```

## Data Cleaning

The following data-quality issues were handled:

- Null values in City column replaced with `Unknown`
- Duplicate transaction IDs removed
- Extra spaces removed from text columns
- Inconsistent transaction type values standardized
- Inconsistent status values standardized
- Incorrect date formats converted to proper date type
- Currency symbols and commas removed from amount columns
- Invalid credit scores handled
- Invalid customer age values handled
- Orphan records identified and handled

## Power BI Dashboard

The interactive Power BI report is available here:

[View the Power BI Dashboard](https://app.powerbi.com/links/yAGZS6f8rA?ctid=56c1d497-700b-49cf-8f8d-3dd6b20d522f&pbi_source=linkShare)

The report contains two pages:

### Page 1: Transaction Performance

This page shows overall transaction performance.

It includes:

- Total Transaction Amount
- Total Transactions
- Average Transaction Amount
- Transaction Success Rate
- Loan Disbursement Amount
- Credit Card Purchase Amount
- Monthly transaction trend
- Transaction type analysis
- Transaction status analysis
- Top products
- Top branches
- Region and branch matrix

### Page 2: Customer, Product & Branch Analysis

This page analyzes customers, products, and branches.

It includes:

- Total Customers
- Total Branches
- Total Products
- Deposit Amount
- Withdrawal Amount
- Fee Income
- Interest Income
- City and state analysis
- Customer segment analysis
- Account type analysis
- Product category analysis
- Branch and region analysis
- Geographic analysis

## KPI Cards

The following KPI cards are included in the Power BI report:

| KPI | Description |
|---|---|
| Total Transaction Amount | Total value of all transactions |
| Total Transactions | Total number of transactions |
| Average Transaction Amount | Average value per transaction |
| Transaction Success Rate | Percentage of successful transactions |
| Loan Disbursement Amount | Total loan amount disbursed |
| Credit Card Purchase Amount | Total credit card purchase amount |
| Total Customers | Number of unique customers |
| Total Branches | Number of unique branches |
| Total Products | Number of unique products |
| Deposit Amount | Total deposit amount |
| Withdrawal Amount | Total withdrawal amount |
| Fee Income | Total fee charge amount |
| Interest Income | Total interest credit amount |

## DAX Measures

Some important DAX measures used in the report:

```dax
Total Transaction Amount =
SUM ( Combined_Transactions[TransactionAmount] )
```

```dax
Total Transactions =
COUNTROWS ( Combined_Transactions )
```

```dax
Average Transaction Amount =
AVERAGE ( Combined_Transactions[TransactionAmount] )
```

```dax
Successful Transactions =
CALCULATE (
    COUNTROWS ( Combined_Transactions ),
    Combined_Transactions[TransactionStatus] = "Success"
)
```

```dax
Transaction Success Rate =
DIVIDE (
    [Successful Transactions],
    [Total Transactions],
    0
)
```

```dax
Loan Disbursement Amount =
CALCULATE (
    [Total Transaction Amount],
    Combined_Transactions[TransactionType] = "Loan Disbursement"
)
```

```dax
Total Customers =
DISTINCTCOUNT ( Combined_Transactions[CustomerName] )
```

## Slicers Used

The dashboard includes the following slicers:

- Year
- MonthName
- TransactionType
- TransactionStatus
- ProductCategory
- Region
- AccountType
- CustomerSegment

## How to Use This Project

1. Download or clone this repository
2. Open the SQL scripts in SQL Server Management Studio
3. Run the scripts to create the database and tables
4. Open the Power BI file
5. Refresh the data
6. Explore the dashboard using slicers and visuals

## Repository Files

```text
README.md
SQL Scripts/
Power BI File/
Dataset/
Screenshots/
```

## Future Improvements

- Add fraud transaction analysis
- Add customer churn analysis
- Add loan default analysis
- Add monthly and yearly comparisons
- Add drill-through pages for customer and branch details
- Add row-level security for branch users

## Author

Created for a SQL Server and Power BI data analytics project.
