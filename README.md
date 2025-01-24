# Sales Analysis

## Table of Contents

- [Project overview](#Project-overview)
- [Data Sources](#Data-Source)
- [Results/Findings](#Results/Findings)



### Project overview

The goal of this project is to analyze sales data from 3 top supermarket stores located in 3 states to uncover patterns, trends, and insights that can hlep the businesses optimize their operations, marketing strategies, and inventory management. The analysis will focus on identifying high-performing products, understanding customer preferences, and providing actionable recommendations for improving sales performance.

![Supermarketstore 2025-01-24 094956](https://github.com/user-attachments/assets/e3893c97-c7e6-4275-afd5-11b92d3be672)

![SupermarketStore 2025-01-24 094848](https://github.com/user-attachments/assets/b8ffe5cd-399b-4f2e-9888-baa6f2ea363b)


### Data source

Sales Data: The primary dataset used for the this analysis is the "Abuja_Branch.csv","Lagos_Branch.csv" and "Port_Harcourt_Branch.csv" containing sales information made by the company

### Tools

- SQL server- for data transformation
- Power BI- for visualization

### Data transformation

1. Combining the three tables using union all
2. Using character index and substring to extract the time from the time column
3. Performimg a column count using information schema
4. Standerdizing the data
5. Craeting view

### Visualization

The visualization process involved exploring the salses data to provide answers to the following questions:

-  Among the items sold,which was most profitable?
-  what is the avarage rating by gender within the three months of sales?
-  What is the three months rolling avarage?
-  what day of the week do we have more sales?
-  Which supermarket store earns most profit?

### Data Analysis

```ALTER VIEW SuperMarket_Standardized AS
SELECT 
    Invoice_ID,
	Product_line,
    CAST(Unit_price AS DECIMAL(10, 2)) AS Unit_price,
    CAST(Quantity AS INT) AS Quantity,
    CAST(Total AS DECIMAL(10, 2)) AS Total,
    CAST(Date AS DATE) AS Date,
    CASE 
        WHEN CHARINDEX('.', CONVERT(VARCHAR, Time)) > 0 
        THEN SUBSTRING(CONVERT(VARCHAR, Time), 1, CHARINDEX('.', CONVERT(VARCHAR, Time)) - 1) 
        ELSE CONVERT(VARCHAR, Time) 
    END AS Time,
    UPPER(Payment) AS Payment,
    UPPER(City) AS City,
    UPPER(Customer_type) AS Customer_type,
    UPPER(Gender) AS Gender,
    CAST(cogs AS DECIMAL(10, 2)) AS cogs,
    CAST(gross_income AS DECIMAL(10, 2)) AS gross_income,
    CAST(Rating AS DECIMAL(3, 1)) AS Rating,
    'Lagos_Branch' AS Source
FROM [SQL_Super_Market_Project].[dbo].Lagos_Branch

UNION ALL

SELECT 
    Invoice_ID,
	Product_line,
    CAST(Unit_price AS DECIMAL(10, 2)) AS Unit_price,
    CAST(Quantity AS INT) AS Quantity,
    CAST(Total AS DECIMAL(10, 2)) AS Total,
    CAST(Date AS DATE) AS Date,
    CASE 
        WHEN CHARINDEX('.', CONVERT(VARCHAR, Time)) > 0 
        THEN SUBSTRING(CONVERT(VARCHAR, Time), 1, CHARINDEX('.', CONVERT(VARCHAR, Time)) - 1) 
        ELSE CONVERT(VARCHAR, Time) 
    END AS Time,
    UPPER(Payment) AS Payment,
    UPPER(City) AS City,
    UPPER(Customer_type) AS Customer_type,
    UPPER(Gender) AS Gender,
    CAST(cogs AS DECIMAL(10, 2)) AS cogs,
    CAST(gross_income AS DECIMAL(10, 2)) AS gross_income,
    CAST(Rating AS DECIMAL(3, 1)) AS Rating,
    'Abuja_Branch' AS Source
FROM [SQL_Super_Market_Project].[dbo].Abuja_Branch

UNION ALL

SELECT 
    Invoice_ID,
	Product_line,
    CAST(Unit_price AS DECIMAL(10, 2)) AS Unit_price,
    CAST(Quantity AS INT) AS Quantity,
    CAST(Total AS DECIMAL(10, 2)) AS Total,
    CAST(Date AS DATE) AS Date,
    CASE 
        WHEN CHARINDEX('.', CONVERT(VARCHAR, Time)) > 0 
        THEN SUBSTRING(CONVERT(VARCHAR, Time), 1, CHARINDEX('.', CONVERT(VARCHAR, Time)) - 1) 
        ELSE CONVERT(VARCHAR, Time) 
    END AS Time,
    UPPER(Payment) AS Payment,
    UPPER(City) AS City,
    UPPER(Customer_type) AS Customer_type,
    UPPER(Gender) AS Gender,
    CAST(cogs AS DECIMAL(10, 2)) AS cogs,
    CAST(gross_income AS DECIMAL(10, 2)) AS gross_income,
    CAST(Rating AS DECIMAL(3, 1)) AS Rating,
    'Port_Harcourt_Branch' AS Source
FROM [SQL_Super_Market_Project].[dbo].Port_Harcourt_Branch;

```

### Results/Findings

1. Abuja store made the most profit in January and February. In March, while health and beauty equipments were sold the most,the product had the highest cost of production.
2. In Abuja store there was a sharp drop in sales in the second and third week. Sales improved in the forth week, possibly driven by payment of month end salary that motivated the team.
3. Abuja store got better rating form the female gender with upto 31.01% of females rating 9.8 on food a beverages.

### Recommendation

- Focus on expanding and promoting products with low cost of production in order to make better profit
- Consistency is key for customer satisfaction and to increase returning customers






