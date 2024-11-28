# Credit Card Weekly Status Report

## Project Objective

To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.

---

## Project Overview

This project focuses on creating a **Credit Card Weekly Status Report** using data analysis tools like SQL and Power BI. The primary goal is to enable stakeholders to:
- Monitor credit card performance.
- Identify trends in customer behavior.
- Analyze revenue and other key metrics efficiently.

---

## Steps to Execute the Project

### 1. Import Data into SQL Database

#### Steps:
1. **Prepare CSV File:**
   - Ensure the data is clean and formatted correctly.
   - Include key columns such as customer details, transactions, and financial metrics.

2. **Create Tables in SQL:**
   - Design a database schema to store the required data.
   - Tables include:
     - Customer details (e.g., customer_age, income).
     - Credit card transaction details (e.g., annual_fees, total_trans_amt).

3. **Import CSV File:**
   - Use SQL tools or scripts to load the data into the created tables.

---

### 2. Data Transformation Using DAX Queries

Below are the custom DAX queries used for analysis:

#### Age Group Categorization
```DAX
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)
```

#### Income Group Categorization
```DAX
IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)
```

#### Weekly Revenue Calculation
```DAX
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

Current_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)

Previous_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
    )
)
```

---

### 3. Build the Credit Card Dashboard

#### Tools Used:
- **Power BI:** To create an interactive and visually appealing dashboard.
- **SQL:** To process and query the imported data.

#### Dashboard Features:
- **Revenue Analysis:**
  - Displays current and previous week’s revenue.
- **Customer Segmentation:**
  - Age groups (e.g., 20-30, 30-40).
  - Income levels (Low, Medium, High).
- **Trend Visualization:**
  - Graphs and KPIs for monitoring weekly trends.

#### Key Outcomes:
- **Actionable Insights:**
  - Shared with stakeholders to support decision-making processes.
- **Efficient Monitoring:**
  - Real-time tracking of key performance metrics.

#### Repository Contents:
- **CSV Data Files:** Used for importing customer and transaction data into SQL.
- **Dashboard Images:**
  - Credit Card Transaction Report.
  - Credit Card Customer Satisfaction Report.

---

## How to Use

1. Clone the repository.
2. Follow the steps in the **Import Data** section to set up your SQL database.
3. Use the DAX queries to prepare calculated columns and measures in Power BI.
4. Build and publish the dashboard for stakeholder access.

---

## Future Enhancements
- Incorporate machine learning models to predict customer behavior.
- Automate data refresh for real-time updates.
- Add more granular filters for better segmentation.

