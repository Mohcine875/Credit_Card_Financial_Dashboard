# Credit Card Weekly Status Dashboard

## Project Objective
The objective of this project is to develop a comprehensive credit card weekly dashboard. This dashboard provides real-time insights into key performance metrics and trends, enabling stakeholders to effectively monitor and analyze credit card operations.

## Table of Contents
1. [Project Objective](#project-objective)
2. [Data from SQL](#data-from-sql)
3. [Data Processing & DAX](#data-processing--dax)
4. [Dashboard & Insights](#dashboard--insights)
5. [Export & Share Project](#export--share-project)
6. [Add to Resume](#add-to-resume)

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
IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
Current_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)
Previous_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]) - 1
    )
)
Dashboard & Insights
Project Insights - Week 53 (31st Dec 2023)

    Week-over-Week Change: Revenue increased by 28.8%.
    Year-to-Date Overview:
        Overall revenue: $57M
        Total interest earned: $8M
        Total transaction amount: $46M
        Male customers contribute more to revenue: $31M vs Female: $26M
        Blue & Silver credit cards account for 93% of overall transactions.
        TX, NY & CA contribute to 68% of total revenue.
        Overall Activation rate: 57.5%
        Overall Delinquency rate: 6.06%

Export & Share Project

The final dashboard can be exported and shared with stakeholders to facilitate data-driven decision-making.
Export the Dashboard as a PDF

    Export as PDF:
        In Power BI Service, open your report.
        Click on File > Export to PDF.
        This will generate a PDF file of the dashboard.
    Save the PDF to the Project Directory:
        Save the exported PDF in your project directory, for example in a docs/ folder.

Share the PDF with Stakeholders

    Attach the PDF in README:
        You can download the detailed PDF report of the dashboard here.
    Share via Email or Online Storage:
        You can also share the PDF file via email or upload it to a cloud storage service like OneDrive, Google Drive, or SharePoint, and then share the link with stakeholders.

Add to Resume

Credit Card Financial Dashboard using Power BI:

    Developed an interactive dashboard using transaction and customer data from a SQL database to provide real-time insights.
    Streamlined data processing and analysis to monitor key performance metrics and trends.
    Shared actionable insights with stakeholders to support informed decision-making processes.

This experience can be highlighted in your resume to showcase your expertise in data analysis, Power BI, and your ability to provide valuable business insights through data-driven decision-making.
