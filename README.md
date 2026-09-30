# 📦 Inventory & Stock Dashboard

## 📊 Project Overview

The **Inventory & Stock Dashboard** is an interactive Business Intelligence project developed using **Microsoft Power BI** to analyze inventory levels, product sales, purchasing activity, supplier performance, and stock movement.

The dashboard helps businesses monitor their inventory, identify low-stock products, understand sales demand, track purchasing costs, and make data-driven inventory management decisions.

---

## 🎯 Business Problem

Businesses need to maintain the right amount of inventory to meet customer demand while avoiding:

* Stockouts
* Excess inventory
* Slow-moving products
* Unnecessary purchasing
* High inventory investment
* Poor replenishment decisions

This project provides a centralized dashboard to monitor these areas and support better inventory planning.

---

## 🎯 Project Objectives

The main objectives of this project are to:

* Monitor current inventory levels
* Identify products below their reorder levels
* Identify top-selling products
* Analyze inventory by category
* Analyze supplier-wise purchase value
* Calculate the value of current inventory
* Measure inventory turnover
* Estimate stock coverage days
* Compare purchasing and sales trends
* Support inventory replenishment decisions

---

# 🗂️ Dataset

The project uses multiple related tables to create a structured Power BI data model.

### 1. Products

Contains product master information.

| Column       | Description               |
| ------------ | ------------------------- |
| ProductID    | Unique product identifier |
| ProductName  | Name of the product       |
| Category     | Product category          |
| UnitCost     | Cost per unit             |
| SellingPrice | Selling price per unit    |
| ReorderLevel | Minimum stock level       |
| SupplierID   | Associated supplier       |

### 2. Suppliers

Contains supplier information.

| Column        | Description                |
| ------------- | -------------------------- |
| SupplierID    | Unique supplier identifier |
| SupplierName  | Supplier name              |
| City          | Supplier location          |
| ContactPerson | Supplier contact           |

### 3. Purchases

Contains purchasing transactions.

| Column     | Description                |
| ---------- | -------------------------- |
| PurchaseID | Unique purchase identifier |
| Date       | Purchase date              |
| ProductID  | Purchased product          |
| SupplierID | Supplier                   |
| Quantity   | Purchased quantity         |
| UnitCost   | Purchase cost per unit     |

### 4. Sales

Contains sales transactions.

| Column       | Description            |
| ------------ | ---------------------- |
| SaleID       | Unique sale identifier |
| Date         | Sales date             |
| ProductID    | Sold product           |
| Quantity     | Quantity sold          |
| SellingPrice | Selling price per unit |

### 5. Inventory

Contains current inventory information.

| Column       | Description             |
| ------------ | ----------------------- |
| ProductID    | Product identifier      |
| CurrentStock | Current available stock |

### 6. Date

A dedicated date table used for time-based analysis.

---

# 🧩 Data Model

The project follows a **star-schema-oriented data model** with dimension and fact tables.

### Dimension Tables

* Products
* Suppliers
* Date

### Fact Tables

* Sales
* Purchases
* Inventory

### Relationships

```text
Suppliers
    │
    ├────────── Products
    │              │
    │              ├──────── Sales
    │              │
    │              ├──────── Purchases
    │              │
    │              └──────── Inventory
    │
    └────────── Purchases

Date
 │
 ├──────── Sales
 │
 └──────── Purchases
```

---

# 📌 Key Performance Indicators (KPIs)

The dashboard tracks the following KPIs:

### Current Stock

Measures the total quantity of inventory currently available.

```DAX
Current Stock =
SUM(Inventory[CurrentStock])
```

### Units Sold

Measures the total quantity of products sold.

```DAX
Units Sold =
SUM(Sales[Quantity])
```

### Purchase Value

Calculates the total value of purchased inventory.

```DAX
Purchase Value =
SUMX(
    Purchases,
    Purchases[Quantity] * Purchases[UnitCost]
)
```

### Sales Value

Calculates the total value of sales.

```DAX
Sales Value =
SUMX(
    Sales,
    Sales[Quantity] * Sales[SellingPrice]
)
```

### Stock Value

Measures the current inventory value based on product cost.

```DAX
Stock Value =
SUMX(
    Inventory,
    Inventory[CurrentStock] *
    RELATED(Products[UnitCost])
)
```

### Low Stock Items

Identifies products whose stock is at or below their reorder level.

```DAX
Stock Status =
IF(
    Inventory[CurrentStock] <=
    RELATED(Products[ReorderLevel]),
    "Low Stock",
    "Healthy"
)
```

```DAX
Low Stock Items =
CALCULATE(
    COUNTROWS(Inventory),
    Inventory[Stock Status] = "Low Stock"
)
```

### COGS

Calculates the cost of goods sold.

```DAX
COGS =
SUMX(
    Sales,
    Sales[Quantity] *
    RELATED(Products[UnitCost])
)
```

### Stock Turnover

Measures how quickly inventory is moving.

```DAX
Stock Turnover =
DIVIDE(
    [COGS],
    [Stock Value]
)
```

### Average Daily Sales

Calculates the average number of units sold per sales day.

```DAX
Average Daily Sales =
DIVIDE(
    [Units Sold],
    DISTINCTCOUNT(Sales[Date])
)
```

### Stock Coverage Days

Estimates how many days the current stock can support sales.

```DAX
Stock Coverage Days =
DIVIDE(
    [Current Stock],
    [Average Daily Sales]
)
```

---

# ❓ Business Questions

The dashboard answers the following business questions:

1. **Which products are currently low in stock?**
2. **Which products sell the most?**
3. **Which categories hold the most inventory?**
4. **Which suppliers account for the highest purchase value?**
5. **How much money is currently tied up in inventory?**
6. **How quickly is inventory moving?**
7. **How many days can current inventory support sales?**

---

# 📊 Dashboard Features

## Inventory Overview

The main dashboard provides:

* Current Stock
* Stock Value
* Units Sold
* Low Stock Items
* Stock Turnover
* Purchase Value
* Stock Coverage Days

### Visualizations

* 📊 Stock by Category
* 📈 Sales vs Purchases Trend
* 🏆 Top 10 Selling Products
* 🏭 Purchase Value by Supplier
* ⚠️ Low Stock Products
* 📦 Inventory Details

### Interactive Filters

Users can filter the dashboard using:

* Date
* Category
* Supplier
* Stock Status

---

# 💡 Business Insights

### Low Stock Products

Products at or below their reorder level require attention and may need replenishment to reduce stockout risk.

### Top-Selling Products

Products with high sales demand should be monitored closely to maintain sufficient inventory availability.

### Inventory by Category

Comparing inventory levels with sales demand helps identify categories that may have relatively high or low inventory.

### Supplier Analysis

Supplier-wise purchase value helps identify suppliers that account for a significant portion of procurement spending.

### Inventory Investment

Stock Value shows the amount of capital currently tied up in inventory.

### Inventory Movement

Stock Turnover helps evaluate how efficiently inventory is being converted into sales.

### Stock Coverage

Stock Coverage Days helps estimate how long current inventory can support sales based on the average daily sales rate.

---

# 🛠️ Tools & Technologies

* **Microsoft Power BI**
* **DAX**
* **Microsoft Excel**
* **Data Modeling**
* **Data Visualization**
* **Business Intelligence**

---

# 🧠 Skills Demonstrated

This project demonstrates practical skills in:

* Data Modeling
* Star Schema Design
* Power BI
* DAX
* KPI Development
* Data Visualization
* Inventory Analysis
* Sales Analysis
* Supplier Analysis
* Business Problem Solving
* Business Intelligence Reporting

---

# 📁 Project Structure

```text
Inventory-Stock-Dashboard/
│
├── Data/
│   ├── Products.csv
│   ├── Suppliers.csv
│   ├── Purchases.csv
│   ├── Sales.csv
│   ├── Inventory.csv
│   └── Date.csv
│
├── PowerBI/
│   └── Inventory_Stock_Dashboard.pbix
│
├── Screenshots/
│   ├── dashboard.png
│   ├── supplier-analysis.png
│   └── inventory-details.png
│
└── README.md
```

---

# 🚀 Future Improvements

Future versions of this project could include:

* Automated inventory alerts
* Demand forecasting
* Sales forecasting
* ABC inventory analysis
* Supplier performance scoring
* Product-level reorder recommendations
* Profitability analysis
* Power BI Service deployment
* Automated data refresh
* Machine Learning-based demand prediction

---

# 📌 Conclusion

The **Inventory & Stock Dashboard** demonstrates how Power BI can transform raw inventory, sales, purchasing, and supplier data into meaningful business insights.

The project focuses on answering practical inventory-management questions and demonstrates the complete BI workflow from **data modeling → DAX calculations → visualization → business insights**.

---

## 👨‍💻 Author

**Lukesh**

B.Tech Artificial Intelligence & Data Science

### Skills

`Power BI` `SQL` `Python` `Excel` `DAX` `Data Analysis` `Business Intelligence`

---

⭐ If you found this project useful, feel free to explore the repository and provide feedback.
