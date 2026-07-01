# 📘 Query and Analyze Lakehouse Data

## 🎯 Overview

After data has been **ingested** and **transformed**, it is ready for analysis.

Microsoft Fabric Lakehouses provide multiple ways to query and analyze data, allowing users to choose the most appropriate tool based on their workflow:

- **SQL Analytics Endpoint** → SQL-based querying
- **Spark Notebooks** → Advanced analytics and data engineering
- **Power BI** → Reporting, dashboards, and business intelligence

---

# 🔍 Query Data Using the SQL Analytics Endpoint

## What is the SQL Analytics Endpoint?

Every Lakehouse automatically includes a **SQL Analytics Endpoint**, providing **read-only** access to Delta Lake tables using **T-SQL**.

It allows users to query data without modifying the underlying files.

---

## Features

- Read-only access
- Uses familiar **T-SQL**
- Queries Delta Lake tables
- Supports SQL Views
- Supports security policies

---

## Common Operations

You can:

- Query data
- Filter rows
- Aggregate values
- Join tables
- Explore datasets

---

## Common Use Cases

### Ad-hoc Queries

Quickly answer business questions by exploring data.

---

### Business Intelligence Connections

Connect tools such as:

- Power BI
- Microsoft Excel
- Azure Data Studio

to analyze Lakehouse data.

---

### Data Validation

Verify data after:

- ETL processes
- Transformations
- Data loading

---

# 📄 SQL Views

## What are SQL Views?

Views store reusable SQL query logic.

They simplify reporting by hiding complex SQL behind a virtual table.

---

## Common Uses

- Apply business rules
- Simplify complex joins
- Filter data
- Create reusable datasets

### Example

A view could:

- Join Sales and Products tables
- Return only active products

This simplifies report development.

---

# 🔐 SQL Security

The SQL Analytics Endpoint supports fine-grained security.

## Row-Level Security (RLS)

Restricts which rows users can view.

---

## Column-Level Security (CLS)

Restricts access to sensitive columns.

---

# 🤖 Copilot for SQL

Copilot can generate **T-SQL** from natural language prompts.

### Benefits

- Faster query writing
- Learn SQL syntax
- Simplify complex queries
- Increase productivity

---

# 🧑‍💻 Query Data Using Spark Notebooks

## What are Spark Notebooks?

Spark Notebooks provide a code-based environment for querying, analyzing, and transforming Lakehouse data.

They support both SQL and Python-based analytics.

---

# Spark SQL vs PySpark

## Spark SQL

Uses standard SQL syntax inside notebook cells.

### Example

```sql
SELECT *
FROM sales.orders;
```

### Best For

- SQL users
- Familiar query patterns
- Data exploration

---

## PySpark

Uses Python with Apache Spark.

Users can:

- Execute SQL with `spark.sql()`
- Manipulate DataFrames
- Use Python libraries

### Common DataFrame Methods

- `select()`
- `filter()`
- `groupBy()`
- `join()`

### Best For

- Complex transformations
- Data engineering
- Machine learning
- Python integration

---

# Common Notebook Use Cases

## Exploratory Data Analysis (EDA)

Analyze:

- Trends
- Outliers
- Patterns
- Relationships

---

## Complex Transformations

Implement business logic that is difficult to express using SQL.

---

## Cross-Workspace Queries

Spark supports querying across multiple Lakehouses.

### Four-Part Namespace

```text
workspace.lakehouse.schema.table
```

Example:

```text
SalesWorkspace.SalesLakehouse.sales.Customers
```

---

# 🤖 Copilot for Notebooks

Copilot assists with:

- Generating PySpark code
- Generating Spark SQL
- Explaining existing code
- Learning Spark syntax

---

# 📊 Analyze and Visualize with Power BI

Power BI is the reporting and business intelligence layer of Microsoft Fabric.

Business users consume Lakehouse data through:

- Interactive reports
- Dashboards
- Semantic Models

---

# Connect Power BI to a Lakehouse

Power BI supports two connection methods.

---

## Option 1: SQL Analytics Endpoint

Connect directly using:

- Power BI
- Excel
- Other SQL-compatible tools

### Best For

- Ad-hoc analysis
- Direct SQL querying
- Data exploration

---

## Option 2: Semantic Model

A Semantic Model references Lakehouse tables and defines:

- Relationships
- Measures
- Business rules
- Calculations

This becomes the foundation for Power BI reports.

---

# 🚀 Direct Lake Mode

When reports use a Lakehouse Semantic Model, Power BI uses **Direct Lake Mode** by default.

---

## How Direct Lake Works

Instead of importing data, Direct Lake:

- Reads Delta Lake Parquet files directly
- Avoids data duplication
- Provides near real-time reporting

---

## Benefits

- Fast performance
- No data imports
- Always reflects current Lakehouse data
- Reduced storage requirements

---

# 🤖 Semantic Models and AI

Semantic Models improve AI-powered experiences.

They define:

- Relationships
- Business logic
- Measures
- Business metrics

This helps Copilot understand organizational data.

---

# Copilot in Power BI

Copilot can:

- Generate reports
- Build visualizations
- Answer business questions
- Interpret Semantic Models

The better the Semantic Model, the better the AI-generated insights.

---

# 🔄 End-to-End Analytics Workflow

```text
Data Sources
      ↓
Lakehouse
      ↓
ETL / Transformations
      ↓
Delta Tables
      ↓
├── SQL Analytics Endpoint
│      ↓
│   SQL Queries
│
├── Spark Notebooks
│      ↓
│   Data Analysis
│
└── Semantic Models
       ↓
   Direct Lake
       ↓
   Power BI Reports
       ↓
 Copilot & AI Insights
```

---

# 📝 Key Takeaways

- Every Lakehouse includes a **SQL Analytics Endpoint** for read-only T-SQL queries.
- SQL Analytics Endpoints support SQL Views, Row-Level Security (RLS), and Column-Level Security (CLS).
- Spark Notebooks support both **Spark SQL** and **PySpark** for advanced analytics.
- PySpark provides greater flexibility for complex transformations and machine learning.
- Spark supports cross-workspace queries using the four-part namespace.
- Copilot assists with SQL and Spark code generation.
- Power BI connects directly to Lakehouse data through SQL Analytics Endpoints or Semantic Models.
- **Direct Lake Mode** enables Power BI to read Delta Lake files directly without importing data.
- Well-designed Semantic Models improve reporting and AI-powered experiences such as Copilot.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| SQL Analytics Endpoint | Read-only T-SQL interface for querying Delta Lake tables |
| T-SQL | Transact-SQL language used for querying Lakehouse tables |
| SQL View | Virtual table containing reusable SQL query logic |
| Row-Level Security (RLS) | Restricts which rows users can access |
| Column-Level Security (CLS) | Restricts access to sensitive columns |
| Spark Notebook | Interactive environment for Spark-based analytics |
| Spark SQL | SQL syntax executed inside Spark Notebooks |
| PySpark | Python API for Apache Spark |
| DataFrame API | PySpark interface for manipulating structured data |
| Semantic Model | Business-friendly model containing relationships and measures |
| Direct Lake | Power BI mode that reads Delta Lake data directly without importing |
| Delta Lake | Open storage format used by Lakehouse tables |
| Copilot | AI assistant that generates SQL, Spark code, reports, and insights |
