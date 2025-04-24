# Data-Analysis-Dashboard
## This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze used car sales data.
## The project involves setting up a used car sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries.

# Project Overview
## Project Title : Used Cars Market Analysis
## Database : cars24_db
# Objectives
## 1.Set up a retail sales database: Create and populate a retail sales database with the provided sales data.
## 2.Data Cleaning: Identify and remove any records with missing or null values.
## 3.Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
## 4.Business Analysis: Use SQL to answer specific business questions and derive insights from the sales data.

# Project Structure
## Database Setup
## . Database Creation: The project starts by creating a database named cars24_db.

``` sql

CREATE DATABASE cars24_db;

USE cars24_db;

CREATE TABLE cars_data (
    Model_Name VARCHAR(255),
    Price INT,
    Manufacturing_Year INT,
    Engine_Capacity INT,
    Spare_Key VARCHAR(10),
    Transmission VARCHAR(20),
    KM_Driven INT,
    Ownership INT,
    Fuel_Type VARCHAR(20),
    Imperfections INT,
    Repainted_Parts INT
);
```
## Data Exploration & Cleaning

   .Record Count: Determine the total number of records in the dataset:
   
   .Customer Count: Find out how many unique car models are in the dataset:
   
   .Category Count: Identify all unique fuel type cars in the dataset:
   
   .Null Value Check: Check for any null values in the dataset and delete records with missing data:

   ``` sql
   SELECT COUNT(*) FROM cars_data;

   SELECT COUNT(DISTINCT Model_Name) FROM cars_data;
   SELECT DISTINCT Fuel_Type FROM cars_data;

SELECT 
    SUM(CASE WHEN Model_Name IS NULL THEN 1 ELSE 0 END) AS model_name_nulls,
    SUM(CASE WHEN Price IS NULL THEN 1 ELSE 0 END) AS price_nulls,
    SUM(CASE WHEN Manufacturing_year IS NULL THEN 1 ELSE 0 END) AS manufacturing_year_nulls,
    SUM(CASE WHEN Engine_capacity IS NULL THEN 1 ELSE 0 END) AS engine_capacity_nulls,
    SUM(CASE WHEN Spare_key IS NULL THEN 1 ELSE 0 END) AS spare_key_nulls,
    SUM(CASE WHEN Transmission IS NULL THEN 1 ELSE 0 END) AS transmission_nulls,
    SUM(CASE WHEN KM_driven IS NULL THEN 1 ELSE 0 END) AS km_driven_nulls,
    SUM(CASE WHEN Ownership IS NULL THEN 1 ELSE 0 END) AS ownership_nulls,
    SUM(CASE WHEN Fuel_type IS NULL THEN 1 ELSE 0 END) AS fuel_type_nulls,
    SUM(CASE WHEN Imperfections IS NULL THEN 1 ELSE 0 END) AS imperfections_nulls,
    SUM(CASE WHEN Repainted_Parts IS NULL THEN 1 ELSE 0 END) AS repainted_parts_nulls
FROM cars_data;
```

## Data Analysis & Findings
## 1. Avarage car price

``` sql
   SELECT 
    AVG(Price) AS avg_price, 
    MIN(Price) AS min_price, 
    MAX(Price) AS max_price
FROM cars_data;

```

. The average car price is ₹5,26,354.
. The cheapest car costs ₹1,39,000, while the most expensive is ₹15,99,000.

## 2.Car depretiation over

``` sql
   SELECT 
    Manufacturing_year, 
    AVG(Price) AS avg_price
FROM cars_data
GROUP BY Manufacturing_year
ORDER BY Manufacturing_year ASC;

```


Older cars (2010-2015) have an average price below ₹5,00,000.
Newer models (2020-2023) have higher resale values, with 2023 models averaging ₹7,75,774


 ## 3. Impact of KM driven on Price


``` sql
SELECT 
    (SUM((KM_driven - avg_km) * (Price - avg_price)) /
    (SQRT(SUM(POW(KM_driven - avg_km, 2))) * 
     SQRT(SUM(POW(Price - avg_price, 2))))) AS correlation_km_price
FROM (
    SELECT 
        KM_driven, 
        Price, 
        (SELECT AVG(KM_driven) FROM cars_data) AS avg_km, 
        (SELECT AVG(Price) FROM cars_data) AS avg_price
    FROM cars_data
) AS subquery;


```

There is a negative correlation (-0.31) between KM driven and Price, meaning higher mileage generally reduces car value.



 ## 4.Fuel Type Trends

 ```sql

  SELECT 
    Fuel_type, 
    COUNT(*) AS count, 
    ROUND((COUNT(*) * 100.0 / SUM(COUNT(*)) OVER ()), 2) AS percentage
FROM cars_data
GROUP BY Fuel_type
ORDER BY count DESC;

```
Petrol cars dominate the market (87.5% of listings).
CNG cars (7.5%) and Diesel cars (5%) are much less common.


## 5.Transmission Type & Pricing

``` sql

SELECT 
    Transmission, 
    AVG(Price) AS avg_price
FROM cars_data
GROUP BY Transmission;
```
Automatic cars sell for a higher average price (₹6,01,339) than Manual cars (₹5,00,358).
## 6.Imperfections & Pricing

``` sql

SELECT 
    Imperfections, 
    AVG(Price) AS avg_price
FROM cars_data
GROUP BY Imperfections
ORDER BY Imperfections ASC;

```
## 7.Repainted Parts & Pricing

``` sql

SELECT 
    Repainted_Parts, 
    AVG(Price) AS avg_price
FROM cars_data
GROUP BY Repainted_Parts
ORDER BY Repainted_Parts ASC;

```

Cars with more imperfections tend to have lower prices.
Repainted parts also slightly reduce car value.


## 8.Car Sales Data Analysis Report

1. ## Introduction
This report analyzes used car sales data to identify pricing trends, depreciation factors, and the impact of various attributes on car value. The dataset consists of 1,445 records and 11 attributes.

# Key Findings

## 2.1 Price Distribution

The average car price is ₹5,26,354.

The cheapest car is priced at ₹1,39,000, while the most expensive is ₹15,99,000.

## 2.2 Car Depreciation Over Time

Older models (2010-2015) have an average price below ₹5,00,000.

Newer models (2020-2023) show higher resale values:

2022 models: ₹7,21,184

2023 models: ₹7,75,774

## 2.3 Impact of Mileage on Price

There is a negative correlation (-0.31) between KM driven and Price.

Higher mileage typically reduces car value, but some exceptions exist.

## 2.4 Fuel Type Trends

Petrol cars dominate the market (87.5% of listings).

CNG cars (7.5%) and Diesel cars (5%) are less common.

## 2.5 Transmission & Pricing

Automatic cars have a higher average price (₹6,01,339) compared to Manual cars (₹5,00,358).

## 2.6 Car Condition & Pricing

Cars with more imperfections tend to have lower prices.

Repainted parts slightly reduce resale value.

## 3. Conclusion & Recommendations

Buyers: Investing in newer models (2020+) ensures better resale value.

Sellers: Maintaining lower mileage and fewer imperfections helps retain value.

Dealers: Automatics are in demand and command a higher price.

This analysis provides actionable insights for car buyers, sellers, and dealerships to make informed decisions.
