# 📘 Model Data in a Warehouse

## 🎯 Overview

Data modeling organizes and structures warehouse data so that it is easy to understand, query, and analyze. Instead of requiring every user to determine table relationships and business logic, a well-designed data model embeds this information directly into the warehouse.

In Microsoft Fabric, data modeling improves:

- T-SQL queries
- Power BI reports
- Semantic Models
- Copilot responses
- Fabric IQ natural language analytics

---

# 🏗️ Prepare Data for Consumption

Before building reports or creating semantic models, prepare the warehouse so consumers only see meaningful business data.

Raw warehouse tables often contain:

- Staging tables
- Surrogate key columns
- ETL artifacts
- Internal processing flags

These objects should generally be hidden from report users.

---

# ✨ Improve the Consumer Experience

## Hide Internal Objects

Hide items that are only used during ETL, such as:

- Staging tables
- Surrogate keys
- ETL columns
- Processing flags

This reduces clutter in reports.

---

## Rename Columns

Use business-friendly names instead of technical abbreviations.

### Example

| Technical Name | Business Name |
|----------------|---------------|
| CustRgn | Customer Region |
| CustID | Customer ID |
| ProdCd | Product Code |

---

## Add Descriptions

Provide descriptions for:

- Tables
- Columns

Descriptions help users understand the data without external documentation.

---

# 🤖 Benefits for AI

Good naming and documentation improve AI-generated results.

AI tools such as:

- Copilot
- Fabric IQ Data Agents

use:

- Table names
- Column names
- Descriptions

to better understand business meaning.

Example:

```text
Customer Region
Description:
Geographic region of the customer's primary address.
```

is much easier for AI to interpret than:

```text
CustRgn
```

---

# 🔗 Understand Relationships

## What is a Relationship?

A relationship connects two tables using shared key columns.

Relationships allow:

- Filtering
- Grouping
- Aggregation
- Automatic joins

---

## Example

```text
FactSales.CustomerKey
        │
        ▼
DimCustomer.CustomerKey
```

This relationship enables analysis such as:

- Sales by Region
- Sales by Customer
- Sales by Segment

---

# 📊 Relationship Properties

## Cardinality

Defines how rows relate between tables.

The most common warehouse relationship is:

### Many-to-One

```text
Many Fact Rows
        │
        ▼
One Dimension Row
```

Example:

Many sales records belong to one customer.

---

## Cross-Filter Direction

Determines how filters flow between tables.

### Recommended

**Single Direction**

```text
Dimension
      ↓
Fact
```

Benefits:

- Predictable filtering
- Better performance
- Simpler model

---

# ⭐ Why Relationships Matter

Without relationships:

- Every query requires manual JOIN statements.
- Business users must understand database structure.
- Reports become inconsistent.

With relationships:

- Joins happen automatically.
- Reports are easier to build.
- AI understands the data model.

Relationships are also used by:

- Power BI
- Copilot
- Fabric IQ

to generate accurate queries.

---

# 📄 Standardize Data Access

Once relationships are established, standardize how users access data.

Microsoft Fabric provides:

- Views
- Measures

---

# 🗂️ Views

## What is a View?

A **View** is a reusable SQL query stored in the warehouse.

It behaves like a virtual table.

---

## Uses

Views can:

- Join tables
- Apply filters
- Hide unnecessary columns
- Present business-friendly datasets

---

## Benefits

- Consistent SQL logic
- Reusable queries
- Simplified reporting
- Stable data source for reports

---

# 📈 Measures

## What is a Measure?

A **Measure** is a reusable **DAX calculation**.

Measures define business metrics once and reuse them across reports.

---

## Common Measures

- Total Sales
- Total Profit
- Average Revenue
- Order Count
- Profit Margin

---

## Benefits

- Single source of truth
- Consistent calculations
- Easier maintenance

When business rules change, only the measure needs updating.

---

# 🧠 Views vs Measures

| Feature | Views | Measures |
|----------|-------|----------|
| Language | T-SQL | DAX |
| Purpose | Standardize data access | Standardize business calculations |
| Used By | SQL users | Power BI reports |
| Returns | Tables | Calculated values |

---

# 📊 Create a Semantic Model

Once the warehouse has:

- Clean tables
- Defined relationships
- Views
- Measures

it is ready for Power BI.

---

## What is a Semantic Model?

A Semantic Model provides a business-friendly layer over warehouse data.

It contains:

- Relationships
- Measures
- Business logic
- Metadata

Power BI reports connect to the Semantic Model instead of directly querying warehouse tables.

---

# ⚡ Direct Lake Mode

Semantic Models created from a Fabric Warehouse use **Direct Lake Mode**.

---

## How Direct Lake Works

Instead of importing data into Power BI:

```text
Warehouse
      ↓
OneLake
      ↓
Power BI
```

Power BI reads data directly from **Delta Lake Parquet files** stored in OneLake.

---

## Benefits

- No scheduled refreshes
- Always current data
- Faster performance
- Reduced storage
- No duplicate datasets

---

# 🤖 Benefits for AI

A well-designed warehouse model improves:

- Copilot
- Fabric IQ
- Power BI
- Natural language analytics

Because AI understands:

- Relationships
- Business names
- Descriptions
- Measures
- Metadata

---

# 🔄 End-to-End Modeling Workflow

```text
Raw Warehouse Tables
          ↓
Hide Internal Objects
          ↓
Rename Columns
          ↓
Add Descriptions
          ↓
Create Relationships
          ↓
Create Views
          ↓
Create Measures
          ↓
Create Semantic Model
          ↓
Direct Lake
          ↓
Power BI Reports
          ↓
Copilot & Fabric IQ
```

---

# 📝 Key Takeaways

- Data modeling makes warehouse data easier to understand and analyze.
- Hide technical objects such as staging tables and surrogate keys from business users.
- Use business-friendly names and descriptions to improve usability and AI understanding.
- Relationships connect Fact and Dimension tables, enabling automatic filtering and aggregation.
- **Many-to-One** relationships and **Single Direction** filtering are recommended for Star Schemas.
- **Views** standardize SQL access by encapsulating joins and business logic.
- **Measures** standardize DAX calculations and provide consistent business metrics.
- Semantic Models provide the reporting layer for Power BI.
- Fabric Warehouse Semantic Models use **Direct Lake Mode**, allowing Power BI to query OneLake data directly without importing it.
- Well-designed models improve analytics, reporting, and AI-powered experiences.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| Data Modeling | Organizing data to simplify analysis and reporting |
| Relationship | Logical connection between two tables |
| Cardinality | Defines how rows relate between tables (e.g., Many-to-One) |
| Cross-Filter Direction | Determines how filters propagate between related tables |
| View | Virtual SQL table that encapsulates reusable query logic |
| Measure | Reusable DAX calculation for business metrics |
| DAX | Data Analysis Expressions language used in Power BI |
| Semantic Model | Business-friendly reporting layer containing relationships, measures, and metadata |
| Direct Lake | Power BI mode that reads Delta Lake files directly from OneLake |
| Fact Table | Stores measurable business events |
| Dimension Table | Stores descriptive business information |
| Surrogate Key | Warehouse-generated key used for relationships |
| Staging Table | Temporary table used during ETL before loading analytical tables |
| Copilot | AI assistant that understands modeled warehouse data |
| Fabric IQ | AI capability that uses metadata, relationships, and semantic models for natural language analytics |
