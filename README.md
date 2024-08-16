# Credit Card Weekly Status Dashboard

## Project Objective
The objective of this project is to develop a comprehensive credit card weekly dashboard. This dashboard provides real-time insights into key performance metrics and trends, enabling stakeholders to effectively monitor and analyze credit card operations.

## Table of Contents
1. [Project Objective](#project-objective)
2. [Data from SQL](#data-from-sql)
3. [Data Processing & DAX](#data-processing--dax)
4. [Dashboard & Insights](#dashboard--insights)

## Data from SQL
1. **Prepare CSV File:** Gather and format the necessary data into CSV files.
2. **Create Tables in SQL:** Set up the required tables in the SQL database.
3. **Import CSV Files into SQL:** Load the CSV data into the SQL database for further processing.

## Data Processing & DAX
### DAX Queries

**Age Group Classification:**
```dax
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)

Income Group Classification:
IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)

Week Number Calculation:
week_num2 = WEEKNUM('public cc_detail'[week_start_date])

Revenue Calculation:
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

Current Week Revenue:
Current_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)

Previous Week Revenue:
Previous_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]) - 1
    )
)

