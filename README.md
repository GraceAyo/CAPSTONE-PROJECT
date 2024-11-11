# CAPSTONE-PROJECT-1
Sales Performance Analysis for a Retail Store

[Overview](#overview)

[Objectives](#objectives)

[Data Source](#data-source)

[Tools Used](#tools-used)

[Data Cleaning and Preparations](#data-cleaning-and-preparations)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

## Overview
This project aim is to analyze and visualize Sales Data using the tools; Excel, SQL Server, and PowerBI. By leveraging these tools, raw data was transformed into actionable insights, providing a comprehensive understanding of sales performance across various dimensions.

## Objectives
- To clean and prepare raw Sales data for analysis.
- To perform data analysis using Excel PivotTables.
- To use SQL Server for advanced querying and data manipulation.
- To visualize the data insights using PowerBI.

## Data source
  The data in this project was sourced from LITA Data Analysis class
  
## Tools Used
- Excel for: [Download Here](https://www.microsoft.com)
  1. Data cleaning
  2. Data preparation
  3. PivotTable analysis
- SQL Server for: [Download SQL Here](https://www.microsoft.com/en/sql-server/sql-server-downloads) and [Download SSMS Here](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16)
  1.  Writing complex queries
  2.  Data retrieving
  3.  Data manipulate
- PowerBI for: [Download Here](https://power-bi-desktop.en.softonic.com/download)
  1. creating interactive dashboards and visualizations.
- GitHub for: [Click Here](https://github.com)
  1. Portfolio Buliding

## Data Cleaning and Preparations
The dataset contained 50,001 rows with columns stated below:
- Order ID
- Customer ID
- Product
- Region
- Order Date
- Quantity
- Unit Price
  
The following steps were taken to clean and prepare the data:
1. Remove Duplicates:
   - Using Excel shortcult "ALT+A" followed by "M", duplicate entries were removed.
   - Out of 50,001 rows, 40,079 duplicates were removed, leaving us with 9,922 unique rows of data
2. Data Transformation:
   - Calculating additional metrics such as;
     - Revenue (Quantity * Unit Price)
     - Average revenue per producr (=AVERAGEIFS(H:H,C:C,J2))
     - Total revenue per region (=SUMIFS(H:H,D:D,L2))
3. Date Formatting:
   - Ensured that all date entries are consistent and correctly formatted.

## Exploratory Data Analysis
### Using Excel:
PivotTables: Created PivotTables to summarize and analyze sales data by Product, Region, and Order Date.
- Calculating total Revenue by Product to identify top-selling items.
- Analyzing the number of unique customers who purchased each product.
- Getting the aggregate quantity of products sold in each region.
- Tracking the total revenue generated on a monthly and yearly basis.
- Summarizing unit price and quantity sold, as well as calculating the average revenue per region.
- Calculating the overall revenue generated from all sales

### Using SQL Server:
Querying Data: Utilized SQL queries to retrieve specific insights from the dataset.
- Total sales for each product category.
  ```sql
  SELECT Product,
  SUM(Revenue) AS TotalSales
  FROM Sales_Data$
  GROUP BY Product;
  
- Number of sales transactions in each region.
  ```sql
  SELECT Region,
  COUNT(OrderID) AS NumberOfTransactions
  FROM Sales_Data$
  GROUP BY Region;
  
- Identified the highest selling product by total sales value.
  ```sql
  SELECT TOP 1 Product,
  SUM(Revenue) AS TotalSales
  FROM Sales_Data$
  GROUP BY Product
  ORDER BY TotalSales DESC;
  
- Calculated total revenue per product.
  ```sql
  SELECT Product,
  SUM(Revenue) AS TotalRevenue
  FROM Sales_Data$
  GROUP BY Product;
  
- Calculated monthly sales totals for the current year.
  ```sql
  SELECT DATEPART(MONTH, OrderDate) AS Month,
  SUM(Revenue) AS MonthlySalesTotal
  FROM Sales_Data$
  WHERE YEAR(OrderDate) = 2024
  GROUP BY DATEPART(MONTH, OrderDate)
  ORDER BY Month;
  
- Identified the top 5 customers by total purchase amount.
  ```sql
  SELECT TOP 5 [Customer Id],
  SUM(Revenue) AS TotalPurchaseAmount
  FROM dbo.Sales_Data$
  GROUP BY [Customer Id]
  ORDER BY TotalPurchaseAmount DESC;

- Calculated the percentage of total sales contributed by each region.
  ```sql
  WITH TotalSales AS (
  SELECT SUM(Revenue) AS TotalSalesValue
  FROM Sales_Data$
  )
  SELECT Region, SUM(Revenue) AS SalesValue,
         (SUM(Revenue) * 100.0 / (SELECT TotalSalesValue FROM TotalSales)) AS SalesPercentage
  FROM Sales_Data$
  GROUP BY Region;

- Identified products with no sales in the last quarter.
  ```sql
  SELECT Product
  FROM Sales_Data$
  GROUP BY Product
  HAVING SUM(CASE
             WHEN OrderDate >= DATEADD(QUARTER, DATEDIFF(QUARTER, 0, GETDATE()) - 1, 0)
             AND OrderDate < DATEADD(QUARTER, DATEDIFF(QUARTER, 0, GETDATE()), 0)
             THEN Quantity
             ELSE 0
             END) = 0;
           

### Dashboard Creation: Developed an interactive dashboard displaying key sales metrics.

Total Sales by Region: A bar chart visualizing sales distribution across regions.

Monthly Sales Trends: A line chart showing sales trends over the months.

Top Products and Customers: Pie charts illustrating top-selling products and top customers by purchase amount.

Sales Contribution by Region: A doughnut chart showing the percentage of total sales contributed by each region.

Interactive Filters: Enabled users to filter data by different dimensions such as date range, product category, and region for deeper insights.

By integrating these tools, the project successfully transformed raw sales data into valuable insights, helping stakeholders make informed decisions based on data-driven analysis.

[Data Visualization](#data-visualization)

## DASHBOARD OVERVIEW ashboard overview
## INSIGHT GENERATION
## RECOMMENDATION
## CONCLUSION
# CAPSTONE-PROJECT-2
