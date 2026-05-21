# 🍽️ Swiggy Sales Case Study using SQL Server

## 📌 Project Overview

This project focuses on analyzing food delivery sales data from Swiggy using SQL Server Management Studio.
The objective is to transform raw transactional data into a clean, structured, and analytics-ready data warehouse using **Data Cleaning**, **Dimensional Modelling**, and **Business KPI Analysis**.

The project demonstrates how SQL can be used for:

* Data validation and cleansing
* Duplicate handling
* Star schema implementation
* KPI generation
* Business intelligence reporting

# 📂 Dataset Description

The raw dataset `swiggy_data` contains food delivery records with details such as:

* State
* City
* Order Date
* Restaurant Name
* Location
* Category/Cuisine
* Dish Name
* Price (INR)
* Rating
* Rating Count


# 🧹 Data Cleaning & Validation

To ensure data quality and accurate analysis, the following validations were performed:

## ✅ Null Checks

Identified missing values in:

* State
* City
* Order_Date
* Restaurant_Name
* Location
* Category
* Dish_Name
* Price_INR
* Rating
* Rating_Count

## ✅ Blank / Empty String Checks

Detected empty or blank fields that could affect reporting accuracy.

## ✅ Duplicate Detection

Duplicate rows were identified using grouping on business-critical columns.

## ✅ Duplicate Removal

Used SQL `ROW_NUMBER()` window function to retain only one unique record while removing duplicate entries.

Example:

SQL Query:

WITH CTE AS (
    SELECT *,
           ROW_NUMBER() OVER (
               PARTITION BY State, City, Order_Date,
                            Restaurant_Name, Location,
                            Category, Dish_Name,
                            Price_INR, Rating, Rating_Count
               ORDER BY Order_Date
           ) AS rn
    FROM swiggy_data
)
DELETE FROM CTE
WHERE rn > 1;


# ⭐ Dimensional Modelling (Star Schema)

To optimize analytical reporting and improve query performance, a **Star Schema** was designed.

## 📌 Dimension Tables

### 📅 dim_date

Contains:

* Year
* Month
* Quarter
* Week

### 📍 dim_location

Contains:

* State
* City
* Location

### 🍴 dim_restaurant

Contains:

* Restaurant_Name

### 🍜 dim_category

Contains:

* Cuisine / Category

### 🍕 dim_dish

Contains:

* Dish_Name

## 📊 Fact Table

### fact_swiggy_orders

Central transactional table containing:

* Price_INR
* Rating
* Rating_Count
* Foreign keys from all dimensions


# 🏗️ Star Schema Architecture


                  dim_date
                      |
                      |
dim_location --- fact_swiggy_orders --- dim_restaurant
                      |
                      |
               dim_category
                      |
                      |
                  dim_dish

# 📈 KPI Development

## 🔹 Basic KPIs

* Total Orders
* Total Revenue (INR Million)
* Average Dish Price
* Average Rating

# 📊 Deep-Dive Business Analysis

## 📅 Date-Based Analysis

* Monthly Order Trends
* Quarterly Order Trends
* Year-wise Growth
* Day-of-Week Order Patterns


## 🌍 Location-Based Analysis

* Top 10 Cities by Order Volume
* Revenue Contribution by States


## 🍽️ Food Performance Analysis

* Top 10 Restaurants by Orders
* Top Cuisine Categories
* Most Ordered Dishes
* Cuisine Performance:

  * Total Orders
  * Average Ratings

## 💰 Customer Spending Insights

Customer spending segmented into buckets:

| Spending Range | Description         |
| -------------- | ------------------- |
| Under 100      | Low spend customers |
| 100–199        | Budget orders       |
| 200–299        | Moderate spend      |
| 300–499        | High-value orders   |
| 500+           | Premium customers   |


## ⭐ Ratings Analysis

Analyzed distribution of dish ratings from:

* 1 ⭐ to 5 ⭐


# 🛠️ Technologies Used

* SQL Server Management Studio
* SQL Server
* T-SQL
* Window Functions
* Common Table Expressions (CTEs)
* Data Warehousing Concepts
* Star Schema Modelling

# 🎯 Key Learnings

Through this project, I gained practical experience in:

* SQL query optimization
* Data cleaning techniques
* Data warehouse design
* Star schema implementation
* KPI reporting
* Business analytics
* Real-world sales analysis

# 🚀 Business Impact

This project helps in:

* Improving reporting efficiency
* Enabling faster analytical queries
* Supporting business decision-making
* Providing scalable analytics architecture
* Delivering meaningful sales and customer insights

# 📌 Future Enhancements

* Power BI Dashboard Integration
* Advanced SQL Optimization
* Predictive Sales Analytics
* Customer Segmentation Models
* Automated ETL Pipelines

# 👩‍💻 Author

**Bhavika Illa**
Aspiring Data Analyst | SQL Enthusiast | Business Intelligence Learner

`SQL` `SSMS` `DataAnalytics` `BusinessIntelligence` `DataWarehouse` `StarSchema` `SwiggyAnalysis` `ETL` `KPIReporting`
