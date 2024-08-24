
# Bike Sharing Data Analysis
---
## Table of Contents
1. [Project Overview](#project-overview)
2. [Data Overview](#data-overview)
3. [Objectives](#objectives)
4. [SQL and DAX Queries](#sql-and-dax-queries)
    - [SQL Queries](#sql-queries)
    - [DAX Queries](#dax-queries)
5. [Power BI Visualization](#power-bi-visualization)
6. [Insights and Recommendations](#insights-and-recommendations)
7. [Machine Learning Applications](#machine-learning-applications)
8. [Conclusion](#conclusion)
9. [Additional Resources](#additional-resources)

## Project Overview
This project analyzes bike-sharing data across two years to identify key revenue drivers, seasonal trends, and customer demographics. The project includes visual dashboards and predictive modeling to enhance profitability.

## Data Overview
- **bike_share_yr_1.csv:** Contains information on bike rentals, including date, customer type, revenue, and other key metrics.
- **cost_table.csv:** Provides cost information related to bike maintenance, operations, and other expenses.

## Objectives
- Analyze revenue trends across different periods (year, season, day).
- Identify profitable customer segments and peak business hours.
- Provide actionable insights for increasing profit margins.
- Utilize predictive analytics to forecast future revenue and profit trends.

## SQL and DAX Queries

### SQL Queries
To demonstrate data extraction and processing, here are some examples:

```sql
-- Create Database and Tables
CREATE DATABASE BikeShareDB;

USE BikeShareDB;

CREATE TABLE BikeShareData (
    Date DATE,
    Customer_Type VARCHAR(50),
    Revenue DECIMAL(10, 2),
    Riders INT,
    Profit_Margin DECIMAL(5, 2)
);

CREATE TABLE CostData (
    Date DATE,
    Cost_Type VARCHAR(50),
    Amount DECIMAL(10, 2)
);

-- Load Data
BULK INSERT BikeShareData
FROM 'path_to_your/bike_share_yr_1.csv'
WITH (FIELDTERMINATOR = ',', ROWTERMINATOR = '\n', FIRSTROW = 2);

BULK INSERT CostData
FROM 'path_to_your/cost_table.csv'
WITH (FIELDTERMINATOR = ',', ROWTERMINATOR = '\n', FIRSTROW = 2);

-- Analyze Revenue by Season
SELECT 
    DATEPART(QUARTER, Date) AS Season,
    SUM(Revenue) AS Total_Revenue
FROM BikeShareData
GROUP BY DATEPART(QUARTER, Date)
ORDER BY Total_Revenue DESC;
```

### DAX Queries
Below are some DAX queries that could be used in Power BI to calculate key metrics:

```dax
-- Total Revenue
TotalRevenue = SUM(BikeShareData[Revenue])

-- Total Profit
TotalProfit = SUMX(BikeShareData, BikeShareData[Revenue] * BikeShareData[Profit_Margin])

-- Revenue by Season
RevenueBySeason = CALCULATE(SUM(BikeShareData[Revenue]), DATEPART(QUARTER, BikeShareData[Date]))

-- Riders by Year
RidersByYear = SUMMARIZE(BikeShareData, BikeShareData[Year], "TotalRiders", SUM(BikeShareData[Riders]))
```

## Power BI Visualization
The Power BI dashboard offers an in-depth look at:

- **Total Revenue and Profit:** Analyzed by year, season, and customer type.
- **KPI Over Time:** Tracking revenue, profit, and riders across months.
- **Revenue by Season:** Visual representation of which seasons generate the most revenue.
- **Rider Demographics:** Breakdown of casual vs. registered riders.

You can view the live Power BI dashboard [here](https://app.powerbi.com/view?r=eyJrIjoiODZlMjMyZjgtYmFhMy00ZWI2LWFmNGQtYjFmZWUxMGFhNTA4IiwidCI6ImI1NWIwM2YzLTIyZmUtNDAyNi1hM2Y0LWQ2NTVjOThiNDAyMCJ9).

## Insights and Recommendations
Based on the visual analysis:

- **Revenue Trends:** Year 2022 saw significant revenue growth, particularly in the summer months (season 3), which generated $3.2M in revenue.
- **Customer Demographics:** Registered users dominate the rider base, contributing over 80% of total rides.
- **Profitability:** Profit margins are consistent across both years, but specific months (like July and August) show peak profitability.
- **Peak Business Hours:** Most profitable hours are between 16h - 18h, with Wednesday and Friday being the most profitable days.
- **Actionable Insight:** Increase marketing efforts during peak seasons and times to maximize revenue. Consider targeted campaigns for casual riders to convert them into registered users.

## Machine Learning Applications

#### Predictive Analytics:
Given the data available, we can apply machine learning techniques such as:

- **Time Series Forecasting:** To predict future revenue and profit trends.
- **Customer Segmentation:** Using clustering algorithms to identify distinct customer segments.
- **Churn Prediction:** Identifying casual riders who are likely to churn and providing them with targeted incentives to retain them.

## Conclusion
This project provides a comprehensive analysis of bike-sharing data, highlighting critical business insights and opportunities for enhancing profitability. By leveraging SQL, DAX, and Power BI, we’ve created a powerful tool for understanding and optimizing bike-sharing operations.

## Additional Resources
- [Download the Dataset](#)
- [View Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiODZlMjMyZjgtYmFhMy00ZWI2LWFmNGQtYjFmZWUxMGFhNTA4IiwidCI6ImI1NWIwM2YzLTIyZmUtNDAyNi1hM2Y0LWQ2NTVjOThiNDAyMCJ9)
---
