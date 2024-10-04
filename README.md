# Credit_Card_Financial_Dashboard

# Project Objective :

To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively. The dashboard supports decision-making in areas like revenue generation, transaction trends, customer segmentation, and credit card activation/delinquency rates.

# Dataset : Financial Dataset

Financial Dataset containing customer details, credit card transaction details, revenue metrics, and geographic data for region-specific analysis.

# Steps :

1. Data Cleaning & Normalization:
   
Performed Data Cleaning: Used Excel to identify and correct inconsistencies, handle missing values, and remove duplicates from the dataset to ensure data accuracy.

Data Normalization:
   
Transformed and normalized the dataset by ensuring consistency in formats (e.g., date formats, number scaling) and standardized categories for analysis (e.g., income ranges, customer age groups).
   
The clean and normalized version of the dataset was then exported to CSV for further processing.

2. Data Importation & Database Setup:
   
MySQL Database: Imported the cleaned and normalized data into a MySQL local server to store structured data tables for efficient querying and future scalability.
Established necessary relationships between tables in the MySQL database, such as linking customer details with transaction and credit card details.

3. Integration with Power BI:
   
Connected Power BI to MySQL: Linked Power BI directly to the MySQL local server to facilitate real-time data synchronization.

By establishing this connection, the Power BI dashboard is automatically updated whenever new data is imported into MySQL, allowing stakeholders to always access the most recent insights.

This integration enabled efficient monitoring of credit card metrics and KPIs without the need for manual data refreshes.

4. Data Transformation & Modeling:
   
Cleaned and transformed data using SQL queries and Power BI's data transformation features.

Created calculated columns for customer segmentation, such as AgeGroup and IncomeGroup, for effective analysis.

Modeled the data using relationships between customer details, credit card details, and transaction tables to ensure accuracy in reporting and analysis.

5. DAX Queries:

Utilized DAX queries to create calculated columns and measures for advanced reporting and insights.

a. Age Group Segmentation:

AgeGroup = SWITCH(
  TRUE(),
  'public cust_detail'[customer_age] < 30, "20-30",
  'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
  'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
  'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
  'public cust_detail'[customer_age] >= 60, "60+",
  "unknown"
)

b. Income Group Segmentation:

IncomeGroup = SWITCH(
  TRUE(),
  'public cust_detail'[income] < 35000, "Low",
  'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
  'public cust_detail'[income] >= 70000, "High",
  "unknown"
)

c. Revenue Calculation:

Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
Current Week Revenue:

d.
Current_week_Reveneue = CALCULATE(
  SUM('public cc_detail'[Revenue]),
  FILTER(
    ALL('public cc_detail'),
    'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
  )
)
Previous Week Revenue:

e.
Previous_week_Reveneue = CALCULATE(
  SUM('public cc_detail'[Revenue]),
  FILTER(
    ALL('public cc_detail'),
    'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
  )
)
Week Number Calculation:

f.
week_num2 = WEEKNUM('public cc_detail'[week_start_date])

6. Dashboard Creation:
   
Designed an interactive Power BI dashboard to visualize KPIs such as weekly revenue, transaction volume, customer growth, and segmentation by age group, income, and geography.

Created KPI cards to display current vs. previous week revenue, transaction counts, and customer data.

Incorporated advanced visualizations like bar charts, line graphs, and pie charts to provide a comprehensive overview of the credit card business operations.

7. Insight Generation:
   
Visualized week-over-week (WoW) revenue trends and customer growth for real-time monitoring.

Created demographic insights by segmenting customers by age and income, and identified which customer groups contribute most to revenue.

Geographic insights were provided by analyzing contributions from key states (TX, NY, CA), which accounted for a significant portion of the total revenue.

8. Business Decision Support:

Shared dashboard insights with key stakeholders to support decision-making in areas such as customer segmentation, transaction growth, and credit card activation strategies.

Recommendations based on insights:

Focus on regions with high revenue contribution (TX, NY, CA) to optimize marketing strategies.

Identify ways to increase customer activation rates (currently at 57.5%) and reduce delinquency (6.06%).

# Insights : 

a. Revenue increased by 28.8% in Week 53 (ending 31st Dec).

b. Total transaction amount and count increased by xx% (specific percentages to be calculated).

c. Customer count increased by xx% (specific percentage to be calculated).

d. Year to Date (YTD) Overview:

e.Total revenue: 57M

f. Interest earned: 8M

g. Total transaction amount: 46M

h. Male customers contributed 31M in revenue, while female customers contributed 26M.

i. 93% of overall transactions were generated by Blue & Silver credit cards.

j. 68% of revenue was generated by customers in TX, NY, and CA.

k. Overall activation rate: 57.5%

l. Delinquent rate: 6.06%


# Action Items : 

a. Monitor Week 54 revenue growth and identify contributing factors.

b. Assess customer engagement by evaluating transaction growth percentages and demographic segmentation.

c. Optimize activation rates by launching targeted campaigns to inactive customers.

d. Implement measures to reduce delinquency rates by strengthening risk management strategies.

