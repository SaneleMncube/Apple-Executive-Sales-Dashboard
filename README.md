# Apple-Executive-Sales-Dashboard

Apple Sales Executive Dashboard - Power BI
An end-to-end Business Intelligence project creating an Executive Sales Dashboard in Power BI Desktop

# Overview
This project demonstrates a complete end-to-end Business Intelligence workflow using Microsoft Power BI. Starting from raw, uncleaned transaction records in Excel, the data undergoes rigorous Extract, Transform, Load (ETL) processing in Power Query, custom feature engineering, data modeling with DAX measures, and culminates in an interactive executive-level sales dashboard.
The dashboard provides C-suite and sales managers with actionable insights into revenue performance, product popularity, platform distribution, and monthly operational trends.

# Key Features
End-to-End Workflow: Data connection, cleaning, modeling, DAX measure creation, visualization, and cloud publishing (Power BI Service).
Executive KPI Tracking: High-level cards tracking Total Revenue, Total Quantity Sold, Total Orders, and Average Sales per Order.
Time-Series Analysis: Dual-metric line chart with an interactive zoom slider to analyze revenue and quantity trends across time.
Top Product Performance: Dynamic bar charts highlighting Top 5 products filtered by total revenue.
Multi-Dimensional Breakdown: Sales distribution across sales platforms (Amazon, Apple Store, Others) and product categories (iPhone, iPad, iMac, etc.).
Conditional Formatting Matrix: Detailed monthly performance grid enriched with background heatmaps and data bars.
Interactive Slicers: Custom tile slicers and dropdowns allowing real-time cross-filtering across platforms, categories, and months.

# Dataset Architecture
The dataset consists of 5,000+ realistic retail transaction records with the following schema:

Column Name	Data Type	Description
Customer ID	Text / ID	Unique identifier for each customer
Invoice ID	Text / ID	Transaction invoice number
Product Name	Text	Specific hardware/accessory item (e.g., iPhone, iMac, iPad)
Category	Text	High-level product grouping
Platform	Text	Sales channel (Amazon, Apple Store, Others)
Quantity	Whole Number	Units purchased per transaction
Unit Price	Currency (Fixed Decimal)	Price per unit prior to discount
Discount Percentage	Decimal Number	Promotional discount applied (0.00 to 1.00)
Date	Date	Date of transaction
Revenue (Custom)	Currency (Fixed Decimal)	Final discounted revenue (Unit Price * Quantity * (1 - Discount))

 # ETL & Data Transformation (Power Query)
Data cleaning and preparation were performed in Power Query Editor to guarantee high data quality before analysis:

Column Quality & Profiling:
Inspected entire dataset profile to evaluate valid, error, and empty rates across all fields.

Handling Missing Values:
Identified and removed null/blank rows in Product Name (reduced record count from 5,006 to 5,002 rows).

Anomaly & Outlier Removal:
Filtered out erroneous negative unit prices by setting a condition: Unit Price >= 0.

Data Type Enforcement:
Formatted monetary fields (Unit Price, Revenue) as Fixed Decimal Number (Currency).
Formatted Quantity as Whole Number and Date as Date.

Feature Engineering:
Calculated Revenue Column: Added custom column in Power Query:
Revenue = [Quantity] * [Unit Price] * (1 - [Discount Percentage])
Chronological Sorting Helper: Created custom Month (MMM YYYY) and MonthSort (YYYYMM) columns to ensure matrix visuals sort chronologically rather than alphabetically.

# DAX Measures
All calculations are centralized within a dedicated Measures table using Data Analysis Expressions (DAX):

// 1. Total Sales / Revenue
Total Sales =
// Sums the net revenue column
SUM('SalesData'[Revenue])

// 2. Total Units Sold
Total Quantity =
// Sums total product units
SUM('SalesData'[Quantity])

// 3. Total Order Volume
Total Orders =
// Counts the total transaction records
COUNTROWS('SalesData')

// 4. Average Order Value
Average Sales =
// Calculates average revenue per order
AVERAGE('SalesData'[Revenue])

# Dashboard Design & Visual Layout
The dashboard adheres to modern executive reporting design principles:

Header Section: Executive title, branded typography (Segoe UI Semibold), grey divider rule, and company logo.
KPI Ribbon: Formatted summary cards with explicit thousand separators, fixed decimal precision (2 places), and soft borders.
Main Visual Canvas:
Line Chart: Sales & Quantity trajectory over time with dynamic zoom slider.
Top 5 Products Bar Chart: Top N filter applied via DAX measures to highlight flagship drivers.
Platform Slicer Tiles: One-click quick filters for sales channels (Amazon, Apple Store, Others).
Monthly Performance Matrix: Cross-tabular grid featuring data bars for unit counts and color fills for revenue density.

# Key Business Insights
Volume & Revenue Correlation: Trend lines show a strong positive correlation between order quantities and overall revenue spikes.
Channel Performance: Slicer analysis reveals sales distribution and performance variations across direct retail (Apple Store) vs. third-party platforms (Amazon).
Core Revenue Drivers: Flagship categories (iPhone & iMac) generate the majority share of total enterprise revenue.

