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

5.1.CREATE DATABASE cars24_db;

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
