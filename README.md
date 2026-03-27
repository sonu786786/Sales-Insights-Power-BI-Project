# 📊 Sales Insights - Data Analysis Project | Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

## 📌 Project Overview

This project simulates a real-world data analysis scenario for **AtliQ Hardware**, a computer hardware business operating across multiple branches in India. The Sales Director faces challenges in tracking sales performance in a rapidly growing market and needs a data-driven solution to replace scattered Excel reports.

The goal is to build an **interactive Power BI dashboard** that provides real-time sales insights, enabling faster and smarter business decisions.

---

## 🧩 Problem Statement

- The Sales Director of AtliQ Hardware struggles to get clear visibility into sales performance across regions.
- Regional managers provide overly optimistic verbal updates, making it hard to track actual numbers.
- Data is spread across multiple Excel files, making consolidation and trend analysis time-consuming and error-prone.
- There is a need for a **single source of truth** — a live dashboard that tells the real story.

---

## 🎯 Project Objectives

- Connect Power BI to a MySQL database containing sales transaction data.
- Perform **data cleaning and ETL** (Extract, Transform, Load) using Power Query.
- Create **DAX measures** for key business metrics.
- Build an **interactive dashboard** with meaningful visualizations.
- Enable the Sales Director to make data-driven decisions at a glance.

---

## 🗂️ Database Schema

The MySQL database (`sales`) contains the following tables:

| Table              | Description                                      |
|--------------------|--------------------------------------------------|
| `customers`        | Customer names and types (Brick & Mortar / E-commerce) |
| `date`             | Date dimension with year, month, and cy_date     |
| `markets`          | Market names and zones (North, South, Central)   |
| `products`         | Product codes and types                          |
| `transactions`     | Sales transactions with amounts, quantities, and currency |

---

## 🔧 Tools & Technologies

| Tool          | Purpose                          |
|---------------|----------------------------------|
| **MySQL**     | Data storage and SQL analysis    |
| **Power BI Desktop** | Data modeling & dashboard  |
| **Power Query** | Data cleaning & transformation |
| **DAX**       | Creating calculated measures     |

---

## 🧹 Data Cleaning Steps (Power Query)

- Removed duplicate and null records from the `transactions` table.
- Filtered out invalid sales amounts (`sales_amount <= 0`).
- Removed transactions outside India (focused on Indian market only).
- Converted currency: USD transactions were normalized to **INR** using a formula.

```m
= Table.AddColumn(#"Filtered Rows", "norm_sales_amount",
    each if [currency] = "USD" then [sales_amount] * 75 else [sales_amount])
```

---

## 📐 DAX Measures

```dax
-- Total Revenue
Revenue = SUM('sales transactions'[norm_sales_amount])

-- Total Sales Quantity
Sales Qty = SUM('sales transactions'[sales_qty])

-- Total Transactions
Total Transactions = COUNTROWS('sales transactions')

-- Profit Margin %
Profit Margin % = DIVIDE([Total Profit Margin], [Revenue], 0)

-- Revenue Contribution %
Revenue Contribution % = DIVIDE([Revenue], CALCULATE([Revenue], ALL('sales customers'), ALL('sales markets')))
```

---

## 📊 Dashboard Views

### 1. 🔑 Key Insights
- Revenue and Sales Quantity KPIs
- Revenue trend over years and months
- Top 5 customers and products by revenue
- Revenue by market

### 2. 💰 Profit Analysis
- Profit margin % by market
- Revenue vs Profit contribution by customer
- Market-level performance comparison

### 3. 📈 Performance Insights
- Year-over-Year revenue comparison
- Revenue contribution % by market and customer segment
- Trend lines for revenue and profit margin

---

## 🗃️ Key SQL Queries

```sql
-- Total revenue in 2020
SELECT SUM(sales_amount)
FROM transactions AS t
INNER JOIN date AS d ON t.order_date = d.date
WHERE d.year = 2020;

-- Revenue from Chennai market in 2020
SELECT SUM(sales_amount)
FROM transactions AS t
INNER JOIN date AS d ON t.order_date = d.date
WHERE d.year = 2020 AND t.market_code = 'Mark001';

-- Distinct products sold in Chennai
SELECT DISTINCT product_code
FROM transactions
WHERE market_code = 'Mark001';
```

---

## 📁 Repository Structure

```
Sales-Insights-PowerBI/
│
├── 📂 data/
│   └── db_dump.sql               # MySQL database dump file
│
├── 📂 pbix/
│   └── sales_insights.pbix       # Power BI report file
│
├── 📂 screenshots/
│   ├── key_insights.png
│   ├── profit_analysis.png
│   └── performance_insights.png
│
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- [MySQL](https://www.mysql.com/downloads/) (v8.0+)
- [Power BI Desktop](https://powerbi.microsoft.com/en-us/downloads/) (Free)

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/Sales-Insights-PowerBI.git
   cd Sales-Insights-PowerBI
   ```

2. **Set up the database**
   - Open MySQL Workbench.
   - Run the `db_dump.sql` file to create and populate the `sales` database.

3. **Connect Power BI to MySQL**
   - Open `sales_insights.pbix` in Power BI Desktop.
   - Go to **Transform Data > Data Source Settings**.
   - Update the MySQL server and database credentials to match your local setup.

4. **Refresh the data** and explore the dashboard!

---

## 📸 Dashboard Preview

> *(Add screenshots of your Power BI dashboard here)*

| Key Insights | Profit Analysis |
|---|---|
| ![Key Insights](screenshots/key_insights.png) | ![Profit Analysis](screenshots/profit_analysis.png) |

---

## 💡 Key Learnings

- How real-world data analysis projects are structured end-to-end.
- Writing SQL queries to explore and validate data.
- Connecting Power BI to a MySQL data source.
- Data transformation using Power Query.
- Writing DAX formulas for business KPIs.
- Building intuitive and interactive dashboards for non-technical stakeholders.

---

## 📬 Contact

**Sonu Kumar**
- GitHub: [@sonu786786](https://github.com/sonu786786)
- LinkedIn: [linkedin.com/in/sonu-kumar51](https://www.linkedin.com/in/sonu-kumar51/)

---

> ⭐ If you found this project helpful, please consider giving it a star!
