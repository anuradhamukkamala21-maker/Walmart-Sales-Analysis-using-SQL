# Walmart Sales Analysis using SQL

## Project Overview

This project explores Walmart's weekly sales data using SQL to identify business trends and generate actionable insights. The dataset contains store-level sales records along with external factors such as temperature, fuel prices, CPI, and unemployment rates.

The primary objective is to transform raw transactional data into meaningful information that can support business decision-making and performance evaluation.

---

## Business Objectives

* Clean and prepare the dataset for analysis
* Analyze overall sales performance across stores
* Identify top-performing and underperforming stores
* Compare sales during holiday and non-holiday periods
* Examine monthly and yearly sales trends
* Evaluate the influence of economic and environmental factors on sales
* Apply advanced SQL techniques for business reporting

---

## Dataset Information

The dataset consists of the following attributes:

| Column       | Description                                           |
| ------------ | ----------------------------------------------------- |
| Store        | Unique store identifier                               |
| Date         | Weekly sales date                                     |
| Weekly_Sales | Revenue generated during the week                     |
| Holiday_Flag | Indicates holiday week (1 = Holiday, 0 = Non-Holiday) |
| Temperature  | Average weekly temperature                            |
| Fuel_Price   | Regional fuel price                                   |
| CPI          | Consumer Price Index                                  |
| Unemployment | Unemployment rate                                     |

---

## Tools & Technologies

* SQL (MySQL / MariaDB)
* phpMyAdmin
* Microsoft Excel
* GitHub

---

## Data Preparation & Cleaning

Before performing the analysis, the dataset was cleaned and validated.

### Data Cleaning Activities

* Imported CSV data into MySQL using phpMyAdmin
* Converted the Date column from text format to DATE datatype
* Verified successful data import
* Checked for missing values
* Checked for duplicate records
* Validated column consistency

### Date Conversion

```sql
UPDATE walmart
SET Date = STR_TO_DATE(Date,'%d-%m-%Y');

ALTER TABLE walmart
MODIFY Date DATE;
```

---

## SQL Analysis Performed

### 1. Total Sales Analysis

Calculated the total revenue generated across all Walmart stores.

```sql
SELECT SUM(Weekly_Sales) AS Total_Sales
FROM walmart;
```

---

### 2. Store Performance Analysis

Evaluated sales performance for each store.

```sql
SELECT Store,
SUM(Weekly_Sales) AS Sales
FROM walmart
GROUP BY Store
ORDER BY Sales DESC;
```

---

### 3. Top 5 Performing Stores

Identified the stores generating the highest sales revenue.

```sql
SELECT Store,
SUM(Weekly_Sales) AS Sales
FROM walmart
GROUP BY Store
ORDER BY Sales DESC
LIMIT 5;
```

---

### 4. Bottom 5 Performing Stores

Identified stores with the lowest sales performance.

```sql
SELECT Store,
SUM(Weekly_Sales) AS Sales
FROM walmart
GROUP BY Store
ORDER BY Sales ASC
LIMIT 5;
```

---

### 5. Holiday vs Non-Holiday Sales

Compared sales performance during holiday and regular periods.

```sql
SELECT Holiday_Flag,
SUM(Weekly_Sales) AS Sales
FROM walmart
GROUP BY Holiday_Flag;
```

---

### 6. Monthly Sales Trend

Analyzed sales patterns across different months.

```sql
SELECT MONTH(Date) AS Month,
SUM(Weekly_Sales) AS Sales
FROM walmart
GROUP BY Month;
```

---

### 7. Temperature Impact Analysis

Studied the relationship between temperature and sales.

```sql
SELECT ROUND(Temperature),
AVG(Weekly_Sales)
FROM walmart
GROUP BY ROUND(Temperature);
```

---

### 8. Unemployment Impact Analysis

Examined how unemployment levels affect sales performance.

```sql
SELECT ROUND(Unemployment),
AVG(Weekly_Sales)
FROM walmart
GROUP BY ROUND(Unemployment);
```

---

### 9. Store Ranking Using Window Functions

Ranked stores according to total sales.

```sql
SELECT Store,
SUM(Weekly_Sales) AS Sales,
RANK() OVER (ORDER BY SUM(Weekly_Sales) DESC) AS Store_Rank
FROM walmart
GROUP BY Store;
```

---

### 10. Moving Average Analysis

Applied moving averages to identify sales trends over time.

```sql
SELECT Date,
Weekly_Sales,
AVG(Weekly_Sales) OVER(
ORDER BY Date
ROWS BETWEEN 4 PRECEDING AND CURRENT ROW
) AS Moving_Avg
FROM walmart;
```

---

## Key Insights

* A small number of stores contribute a substantial share of total revenue.
* Holiday periods demonstrate noticeable changes in sales behavior.
* Monthly sales trends reveal seasonal demand patterns.
* External factors such as temperature and unemployment show measurable relationships with sales performance.
* Certain stores consistently underperform and may require strategic attention.
* Store rankings help identify high-value business locations.

---

## Conclusion

This project demonstrates the practical application of SQL for data cleaning, transformation, aggregation, and business analysis. Through structured querying and exploratory analysis, meaningful insights were extracted from Walmart's sales data to support data-driven decision-making.

The project highlights proficiency in SQL, database management, analytical thinking, and business intelligence concepts.

---

## Author

**Anuradha Mukkamala**

MBA Student | Aspiring Business Analyst | Marketing Analyst
