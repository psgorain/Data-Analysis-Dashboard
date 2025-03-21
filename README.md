# Data-Analysis-Dashboard
This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze used car sales data. The project involves setting up a used car sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries.

# Project Overview
## Project Title : Used Cars Market Analysis
## Database : cars24_db
# Objectives
1. Set up a retail sales database: Create and populate a retail sales database with the provided sales data.
2. Data Cleaning: Identify and remove any records with missing or null values.
3. Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
4. Business Analysis: Use SQL to answer specific business questions and derive insights from the sales data.

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
##2.Data Exploration & Cleaning

   Record Count: Determine the total number of records in the dataset.
   Customer Count: Find out how many unique car models are in the dataset.
   Category Count: Identify all unique fuel type cars in the dataset.
   Null Value Check: Check for any null values in the dataset and delete records with missing data.

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
