# 🏞️ Create a Microsoft Fabric Lakehouse

## 📖 Overview

Traditional analytics solutions were built using **data warehouses**, where structured data is stored in relational tables and queried using SQL.

As organizations began generating **big data** (high volume, variety, and velocity), **data lakes** became popular because they store data as files without requiring a predefined schema.

A **Lakehouse** combines the strengths of both approaches:

- 📂 Data is stored as files in a data lake.
- 🗄️ A relational metadata layer enables SQL querying.
- ⚡ Supports both Apache Spark and SQL workloads.

In **Microsoft Fabric**, a Lakehouse provides:

- **OneLake** storage (built on Azure Data Lake Storage Gen2)
- A **Delta Lake** metastore
- SQL querying capabilities
- Scalable storage and analytics

---

## 🎯 Objectives

In this lab, you will learn how to:

- Create a Microsoft Fabric workspace
- Create a Lakehouse
- Upload files into OneLake
- Explore shortcuts
- Load CSV data into Delta tables
- Query data using SQL
- Build visual SQL queries
- Clean up Fabric resources

---

## ⏱ Estimated Time

**30 minutes**

---

## 📋 Prerequisites

- Microsoft Fabric account
- Fabric Trial, Premium, or Paid Capacity

---

# Part 1 — Create a Workspace

1. Open Microsoft Fabric:

   https://app.fabric.microsoft.com/home?experience=fabric

2. Sign in using your Fabric account.

3. Select **Workspaces** from the left navigation pane.

4. Create a new workspace.

Choose any name, for example:

```text
DataEngineering
```

5. Under **Advanced**, select a licensing mode that includes Fabric capacity:

- Fabric Trial
- Fabric
- Power BI Premium

6. Open the new workspace.

The workspace should initially be empty.

---

# Part 2 — Create a Lakehouse

Inside the workspace:

1. Select **Create**.

> **Note**
>
> If **Create** is not visible, select the **... (More)** menu first.

2. Under **Data Engineering**, select:

```text
Lakehouse
```

3. Give the Lakehouse a unique name.

Example:

```text
salesdata
```

Wait until the Lakehouse is created.

The Lakehouse Explorer contains:

- **Tables**
- **Files**

### Tables

Stores Delta Lake tables that can be queried using SQL.

### Files

Stores files in OneLake that are not managed Delta tables.

You can also create shortcuts here.

Initially, both folders are empty.

---

# Part 3 — Download Sample Data

Download the sample dataset:

https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv

Save it locally as:

```text
sales.csv
```

> **Tip**
>
> Open the URL in a browser, right-click the page, and choose **Save As**.

---

# Part 4 — Upload the CSV File

Inside the Lakehouse Explorer:

Open:

```text
Files
```

Click:

```text
...
→ New Subfolder
```

Create a folder named:

```text
data
```

Open the new folder.

Click:

```text
...
→ Upload
→ Upload Files
```

Upload:

```text
sales.csv
```

After uploading:

- Open **Files/data**
- Verify the file exists
- Select the file to preview its contents

---

# Part 5 — Explore Shortcuts

Shortcuts allow your Lakehouse to reference data stored elsewhere without copying it.

Inside the **Files** folder:

Click:

```text
...
→ New Shortcut
```

Review the available shortcut source types.

Do **not** create a shortcut.

Close the dialog.

---

# Part 6 — Load the CSV into a Delta Table

Navigate to:

```text
Files/data
```

Locate:

```text
sales.csv
```

Click:

```text
...
→ Load to Tables
→ New Table
```

Table name:

```text
sales
```

Choose file type:

```text
CSV
```

Confirm the load operation.

Wait until the table finishes loading.

> **Tip**
>
> If the table does not appear automatically:
>
> ```text
> Tables
> → Refresh
> ```

Open the **sales** table.

Review:

- Data preview
- Schema

---

# Part 7 — View Delta Files

Inside the **sales** table:

Click:

```text
...
→ View Files
```

Notice:

- Parquet files
- `_delta_log`

The `_delta_log` folder records every transaction made to the Delta table.

---

# Part 8 — Query Data Using SQL

At the top-right of the Lakehouse page:

Switch from:

```text
Lakehouse
```

to:

```text
SQL Analytics Endpoint
```

Wait until the SQL interface loads.

Click:

```text
New SQL Query
```

Run the following query:

```sql
SELECT
    Item,
    SUM(Quantity * UnitPrice) AS Revenue
FROM sales
GROUP BY Item
ORDER BY Revenue DESC;
```

Click:

```text
Run
```

The results display total revenue for each product.

---

## Optional SQL Snippets

If you're using a lab VM and cannot easily type SQL, download:

https://github.com/MicrosoftLearning/mslearn-fabric/raw/main/Allfiles/Labs/01/Assets/01-Snippets.txt

Copy and paste the SQL from that file.

---

# Part 9 — Create a Visual Query

Expand:

```text
New SQL Query
```

Choose:

```text
New Visual Query
```

Drag the **sales** table into the visual query designer.

---

## Choose Columns

Open:

```text
Manage Columns
→ Choose Columns
```

Keep only:

- SalesOrderNumber
- SalesOrderLineNumber

Remove every other column.

---

## Group the Data

Open:

```text
Transform
→ Group By
```

Use the following settings:

| Setting | Value |
|----------|-------|
| Group By | SalesOrderNumber |
| New Column | LineItems |
| Operation | Count Distinct Values |
| Column | SalesOrderLineNumber |

The results display the number of line items for each sales order.

---

# Part 10 — Clean Up Resources

Delete the workspace when finished.

Inside the workspace:

Open:

```text
Workspace Settings
```

Navigate to:

```text
General
```

Select:

```text
Remove this Workspace
```

Confirm deletion.

---

# ✅ Summary

In this exercise, you learned how to:

- Create a Microsoft Fabric workspace
- Create a Lakehouse
- Upload files into OneLake
- Explore Lakehouse folders
- Understand shortcuts
- Load CSV files into Delta tables
- Explore Delta Lake files
- Query Lakehouse tables using SQL
- Create visual SQL queries
- Remove Fabric resources after completing the lab
