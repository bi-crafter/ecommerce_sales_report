Project Overview

This project showcases an end-to-end data pipeline, transforming raw, complex transactional data from the Brazilian Olist E-commerce platform into a robust Star Schema model within SQL Server and deploying an advanced, analytically driven performance dashboard in Power BI.

The goal was to solve classic data challenges—denormalization, inconsistent keys, and time-intensive lookups—to deliver a high-performance reporting solution capable of supporting Year-over-Year (YoY) analysis, delivery logistics efficiency, and high-value customer segmentation.

🛠️ Technical Stack

Category

Tool

Description

Data Modeling/ETL

SQL Server (T-SQL)

Used to build permanent, optimized VIEWs that define the Star Schema.

Data Analysis/BI

Power BI

Visualization layer and environment for creating complex business measures.

Advanced Logic

DAX (Data Analysis Expressions)

Used for Time Intelligence, Ratio Analysis, and Context Filtering.

⚙️ Data Engineering & Modeling (SQL Server)

The core challenge was transforming 7+ denormalized raw tables into an optimized Star Schema. This demonstrates expertise in creating a Single Source of Truth (SSOT) for analytics.

1. Star Schema Design Principles

The final model consists of one central fact table and three optimized dimension tables. Crucially, this model was built directly from the raw tables, bypassing the need for an intermediate master view.

Component

Purpose

Key SQL Functions Used

Fact_Orders

Central transactional table containing metrics (Total_Order_Value, Delivery_Delay_Days).

JOIN, DATEDIFF, ISNULL (for cleanup).

Dim_Time

Time hierarchy dimension for date slicing.

CAST (to DATE), DATEPART, DATENAME.

Dim_Product

Standardized product categories.

LEFT JOIN (to translation table), DENSE_RANK() (to create a surrogate key).

Dim_Customer

Unique customer entities.

DISTINCT on customer_unique_id (ensuring unique PK for the "One" side of the relationship).

2. Advanced T-SQL Techniques Showcased

Surrogate Key Generation: Used DENSE_RANK() in Dim_Product to create a numeric Product_Category_Key, ensuring efficient integer-based joins in the Fact table instead of slow string-based lookups.

Data Integrity & Cleansing: Handled NULL values in product translations and review scores using ISNULL() to ensure measures remain accurate.

Performance Optimization: Used CREATE VIEWs to abstract complex join logic, allowing Power BI to query only the necessary, pre-processed analytical layer.

📈 Power BI & Advanced DAX Analytics

The Power BI layer focused on advanced analytical measures and robust segmentation that cannot be done efficiently in SQL.

1. Demonstrated DAX Expertise (Filtering & Context)

The dashboard logic relies on measures that manipulate filter context:

Measure

DAX Functionality

Business Insight

[YoY Revenue Growth %]

CALCULATE, SAMEPERIODLASTYEAR, DIVIDE

Time Intelligence: Provides accurate performance comparison against the prior year's period.

[On-Time Delivery Rate %]

CALCULATE, FILTER

Context Filtering: Calculates the percentage of orders delivered where Delivery_Delay_Days <= 0, isolating the subset of successful deliveries.

Top_Customer_Flag (Calculated Column)

RANKX, ALL, COUNTROWS

Advanced Segmentation: Ranks all customers by Lifetime Value (CLV) and flags the Top 10%, creating a high-value filter for the entire report.

2. Dashboard Design & Reporting

The final dashboard layout follows modern BI design principles:

Visual Hierarchy: Top-row KPI cards (Total Revenue, YoY Growth %, Avg Review Score) provide an immediate health check.

Actionable Insights: Prominent visuals showing product category performance and geographical revenue concentration.

User Empowerment: The use of the Top_Customer_Flag slicer allows business users to instantly analyze the purchasing behavior and logistics performance only for their most valuable customer segment.
