📊 Super Store Sales Dashboard (2019–2020)

End-to-End Business Intelligence Project

This project delivers a complete BI dashboard covering sales performance from 2019–2020. It includes KPI tracking, advanced DAX measures, a clean data model, and interactive visual analytics.


✅ 1. Dashboard Overview
1.1 Key KPIs

Total Orders: Count of all customer orders

Total Sales: Total revenue

Total Profit: Net profit after cost deductions

Average Ship Days: Average time between order date and ship date

1.2 Visuals Included

Donut Charts (3):

Sales by Payment Mode

Sales by Region

Sales by Customer Segment

Line Charts (2):

Monthly Sales Trend

Monthly Profit Trend

Clustered Bar Charts (2):

Sales by Category

Sales by Sub-Category

🧹 2. Data Cleaning Process
2.1 Initial Checks

Imported raw data

Removed duplicate Order IDs

Checked for missing values

Validated all data types

2.2 Data Quality Fixes

Missing Values

Postal Code → Filled with “Unknown”

Ship Date → Removed 0.3% empty records

Product Sub-Category → Verified with product master

Data Type Corrections

Order Date, Ship Date → Converted to date format

Sales & Profit → Converted to numeric (2 decimals)

Outlier Handling

Reviewed negative profit records (discounts/returns)

Validated high sales values (>10,000)

Confirmed ship days >30 for international orders

2.3 Transformations

Added Ship Days = Ship Date – Order Date

Extracted Year, Month, Month-Year

Cleaned Region names

Standardized Payment Modes

🏗️ 3. Data Modeling
3.1 Star Schema

Fact Table – Sales_Fact

Order_ID

Customer_ID

Product_ID

Date_ID

Region_ID

Payment_ID

Sales_Amount

Profit_Amount

Quantity

Discount

Ship_Days

Dimension Tables

Dim_Date → Calendar fields

Dim_Customer → Customer attributes

Dim_Product → Category & Sub-Category

Dim_Region → Regions

Dim_Payment → Payment methods

3.2 Relationships

All fact-to-dimension → Many-to-One, Single direction

📐 4. DAX Measures
4.1 Core KPIs
Total Orders = COUNTROWS(Sales_Fact)

Total Sales = SUM(Sales_Fact[Sales_Amount])

Total Profit = SUM(Sales_Fact[Profit_Amount])

Avg Ship Days = AVERAGE(Sales_Fact[Ship_Days])

4.2 Advanced Measures

Profit Margin

Profit Margin % =
DIVIDE([Total Profit], [Total Sales], 0) * 100


Year-over-Year Sales Growth

YoY Sales Growth % =
VAR CY = [Total Sales]
VAR PY =
    CALCULATE([Total Sales], DATEADD(Dim_Date[Full_Date], -1, YEAR))
RETURN DIVIDE(CY - PY, PY, 0) * 100

4.3 Time Intelligence
Sales 2019 = CALCULATE([Total Sales], Dim_Date[Year] = 2019)
Sales 2020 = CALCULATE([Total Sales], Dim_Date[Year] = 2020)

Profit 2019 = CALCULATE([Total Profit], Dim_Date[Year] = 2019)
Profit 2020 = CALCULATE([Total Profit], Dim_Date[Year] = 2020)


Month-over-Month Sales Growth

MoM Sales Growth % =
VAR CM = [Total Sales]
VAR PM =
    CALCULATE([Total Sales], DATEADD(Dim_Date[Full_Date], -1, MONTH))
RETURN DIVIDE(CM - PM, PM, BLANK()) * 100

4.4 Category Insights
Category Sales =
CALCULATE([Total Sales], ALLSELECTED(Dim_Product[Category]))

SubCategory Sales =
CALCULATE([Total Sales], ALLSELECTED(Dim_Product[Sub_Category]))

4.5 Conditional Formatting
Profit Color =
SWITCH(
    TRUE(),
    [Total Profit] > 100000, "Green",
    [Total Profit] > 50000, "Yellow",
    "Red"
)

🔍 5. Dashboard Insights
5.1 Business Performance

Quick overview of overall sales and profit

Trends help track business growth

KPIs support fast decision-making

5.2 What Users Can Analyze

Payment method performance

Region-wise insights

Customer segment contribution

Category and Sub-Category trends

Sales & profit trends across 24 months

Shipping efficiency

5.3 Business Benefits

Better planning via yearly comparisons

Quick identification of delays in shipping

Improved customer targeting

Smarter inventory and product planning

Data for financial forecasting

🎨 6. Dashboard Design & Best Practices
6.1 Design Principles

Simple and clear layout

Uniform theme

Interactive filters

Optimized DAX for fast performance

Responsive design for all screens

6.2 Best Practices Used

Proper star schema

Dedicated date table

Organized measure tables

Consistent naming

Full documentation for long-term maintenance

🚀 7. Future Enhancements
7.1 New Metrics

Customer Lifetime Value

Product Return Rate

Customer Acquisition Cost

Average Order Value

7.2 Advanced Features

Predictive sales forecasting

Anomaly detection

What-If analysis

Real-time refresh

7.3 New Visuals

Regional heat maps

Customer cohorts

Product association analysis

Seasonal trend analysis

🧾 8. Conclusion

The Super Sales Dashboard brings all key insights into one place, using clean data, a strong model, and well-designed DAX. It follows industry standards and is built to scale, making it easy to extend and customize as business needs grow.

📘 Appendix A — Data Dictionary
Table	Column	Type	Description
Sales_Fact	Order_ID	Text	Unique order ID
Sales_Fact	Sales_Amount	Decimal	Total sales
Sales_Fact	Profit_Amount	Decimal	Net profit
Sales_Fact	Ship_Days	Integer	Delivery days
Dim_Date	Year	Integer	Calendar year
Dim_Date	Month_Name	Text	Month name
Dim_Product	Category	Text	Product category
Dim_Product	Sub_Category	Text	Sub-category
Dim_Customer	Segment	Text	Customer segment
Dim_Region	Region_Name	Text	Region
Dim_Payment	Payment_Mode	Text	Payment type
⏱️ Appendix B — Refresh Schedule

Recommended Refresh

Production → Daily at 6 AM

Development → On demand

Historical Loads → Quarterly full refresh

Data Sources

ERP (Direct connection)

CRM (API)

Shipping System (CSV import)
