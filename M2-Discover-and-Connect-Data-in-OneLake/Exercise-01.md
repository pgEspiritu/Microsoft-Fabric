# 🌊 Discover and Connect to Data in OneLake

## 📖 Overview

In modern analytics organizations, data is often distributed across multiple workspaces and teams:

- Data engineers create **Lakehouses** with raw and cleaned data.
- Business teams create **Warehouses** with business metrics.
- Analysts build **Semantic Models** for reporting.

As an Analytics Engineer, you need to discover and connect to these datasets before transforming or analyzing them.

Microsoft Fabric provides the **OneLake Catalog**, which allows you to:

- Search data assets
- View metadata
- Discover available datasets
- Connect through shortcuts
- Query data using SQL
- Explore semantic models

---

## 🎯 Objectives

In this lab, you will learn how to:

- Create a Fabric workspace
- Create a Lakehouse
- Upload sample data
- Load data into Delta tables
- Discover data using OneLake Catalog
- Explore Lakehouse tables
- Create shortcuts between Lakehouses
- Query data using SQL Analytics Endpoint
- Create Semantic Models
- Explore data visually
- (Optional) Use Copilot to generate SQL
- Clean up resources

---

## ⏱ Estimated Time

**30 minutes**

---

## 📌 Prerequisites

- Microsoft Fabric account
- Fabric Trial or Paid Capacity

---

# Part 1 — Create a Workspace

1. Open Microsoft Fabric:

   https://app.fabric.microsoft.com/home?experience=fabric

2. Sign in.

3. Select **Workspaces**.

4. Create a new workspace.

Example:

- Data-Engineering

5. Under **Advanced**, choose:

- Fabric
- Fabric Trial
- Power BI Premium

6. Wait until the workspace opens.

The workspace should initially be empty.

---

# Part 2 — Create a Lakehouse

Inside the workspace:

1. Select **+ New item**
2. Choose **Lakehouse**
3. Name it:

```
salesdata
```

Wait until the Lakehouse is created.

You should see:

- Tables
- Files

---

# Part 3 — Download Sample Data

Download:

https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv

Save as:

```
sales.csv
```

---

# Part 4 — Upload CSV File

Inside the Lakehouse:

1. Select **Files**
2. Click **...**
3. Choose:

```
Upload
→ Upload files
```

4. Select:

```
sales.csv
```

After upload:

- Open the file
- Preview the contents

---

# Part 5 — Load CSV into a Delta Table

Expand:

```
Files
```

Locate:

```
sales.csv
```

Click:

```
...
→ Load to Tables
→ New table
```

Table name:

```
sales
```

Wait for the loading process.

If needed:

```
Tables
→ Refresh
```

Open the **sales** table to verify:

- Data preview
- Schema

---

# Part 6 — Browse the OneLake Catalog

Return to the Fabric Home page.

Open:

```
OneLake Catalog
```

Select:

```
Explore
```

Filter:

```
Data Items
```

Locate your Lakehouse:

```
salesdata
```

Open its details.

Review metadata including:

- Workspace
- Last Updated
- Owner
- SQL Connection String

Select:

```
Open
```

---

# Part 7 — Explore Lakehouse Tables

Inside the Lakehouse:

Expand:

```
Tables
```

Open:

```
sales
```

Observe:

- Data preview
- Column names
- Data types

Columns include:

- SalesOrderNumber
- SalesOrderLineNumber
- OrderDate
- CustomerName
- EmailAddress
- Item
- Quantity
- UnitPrice
- TaxAmount

Switch to:

```
File View
```

Notice:

- Parquet files
- `_delta_log`

The `_delta_log` stores transaction history for Delta Lake.

---

# Part 8 — Create Another Lakehouse

Return to the workspace.

Create another Lakehouse.

Example name:

```
analytics
```

This Lakehouse will consume data without copying it.

---

# Part 9 — Create a Shortcut

Inside the **analytics** Lakehouse:

```
Tables
→ ...
→ New Shortcut
```

Choose:

```
OneLake
```

Select:

Workspace:

```
Data-Engineering
```

Lakehouse:

```
salesdata
```

Folder:

```
Tables
```

Table:

```
sales
```

Click:

```
Next
→ Create
```

After creation, the **sales** table will display a shortcut icon.

The shortcut references the original table without copying the data.

---

# Part 10 — Query Data with SQL Analytics Endpoint

Inside the **analytics** Lakehouse:

Switch from:

```
Lakehouse
```

to

```
SQL Analytics Endpoint
```

Select:

```
New SQL Query
```

Run:

```sql
SELECT
    Item,
    SUM(Quantity * UnitPrice) AS TotalRevenue,
    SUM(Quantity) AS TotalQuantity
FROM sales
GROUP BY Item
ORDER BY TotalRevenue DESC;
```

This query returns:

- Total revenue
- Total quantity sold
- Grouped by item

---

Run another query:

```sql
SELECT TOP 5
    CustomerName,
    SUM(Quantity) AS TotalQuantity,
    SUM(Quantity * UnitPrice) AS TotalRevenue
FROM sales
GROUP BY CustomerName
ORDER BY TotalRevenue DESC;
```

This returns the top five customers by revenue.

---

# Part 11 — Create a Semantic Model

While still inside the SQL Analytics Endpoint:

Select:

```
New Semantic Model
```

Verify:

```
sales
```

is selected.

Name:

```
Sales Analysis
```

Click:

```
Create
```

The semantic model appears in the workspace.

---

# Part 12 — Explore the Semantic Model

Locate:

```
Sales Analysis
```

Select:

```
...
→ Explore this data
```

Inside the Explore window:

Drag:

```
Item
```

to the canvas.

Drag:

```
Quantity
```

to **Values**.

Change visualization to:

- Bar Chart
- Column Chart

Experiment with additional fields and visualizations.

---

# Part 13 (Optional) — Use Copilot

If Copilot is available:

Open:

```
SQL Analytics Endpoint
```

Create a new SQL query.

Open:

```
Copilot
```

Prompt:

```
Write a SQL query to show total revenue by month for the year 2026, sorted by month.
```

Copilot may generate:

```sql
SELECT
    FORMAT(OrderDate, 'yyyy-MM') AS Month,
    SUM(Quantity * UnitPrice) AS TotalRevenue
FROM sales
WHERE YEAR(OrderDate) = 2026
GROUP BY FORMAT(OrderDate, 'yyyy-MM')
ORDER BY Month;
```

Insert and run the query.

You can also ask Copilot:

- Show me the average unit price by item
- Find all orders with quantity greater than 10

---

# Part 14 — Clean Up Resources

Delete the created workspaces.

For each workspace:

```
Workspace
→ Workspace Settings
→ General
→ Remove this workspace
```

Repeat for:

- Data-Engineering
- analytics

---

# ✅ Summary

In this exercise, you learned how to:

- Create a Fabric workspace
- Create a Lakehouse
- Upload CSV data
- Load Delta tables
- Browse the OneLake Catalog
- Explore Lakehouse metadata
- Create OneLake shortcuts
- Query data using SQL Analytics Endpoint
- Build a Semantic Model
- Explore data visually
- Use Copilot to generate SQL (optional)
- Clean up Fabric resources

Actual Exercise Link: https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/25-discover-onelake.html#clean-up-resources
