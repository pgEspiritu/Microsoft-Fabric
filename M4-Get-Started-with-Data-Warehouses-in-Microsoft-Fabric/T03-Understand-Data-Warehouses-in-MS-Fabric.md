# 📘 Understand Data Warehouses in Microsoft Fabric

## 🎯 Overview

A **Microsoft Fabric Data Warehouse** is a **fully managed, enterprise-scale relational database** built on **OneLake**. It provides **full transactional T-SQL support**, making it ideal for storing, transforming, and analyzing structured business data.

Unlike the **SQL Analytics Endpoint**, which is read-only, a Fabric Data Warehouse supports both **read** and **write** operations while integrating seamlessly with other Fabric workloads.

---

# 🏢 What is a Fabric Data Warehouse?

A Fabric Data Warehouse is a cloud-based relational database designed for analytics.

## Features

- Fully managed infrastructure
- Enterprise-scale performance
- Full transactional T-SQL support
- Data stored in **Delta format**
- Native integration with **OneLake**

---

# 🌊 Built on OneLake

Warehouse data is stored in **Delta format** within **OneLake**.

## Benefits

- Shared storage across Fabric
- No data duplication
- Centralized governance
- Accessible by other Fabric workloads

---

# 💻 Full Transactional T-SQL Support

Fabric Data Warehouses support both **DDL (Data Definition Language)** and **DML (Data Manipulation Language)**.

---

## DDL Statements

Used to define database objects.

Supported commands include:

- `CREATE`
- `ALTER`
- `DROP`

---

## DML Statements

Used to manipulate data.

Supported commands include:

- `INSERT`
- `UPDATE`
- `DELETE`
- `MERGE`

All operations support **ACID transactions** for reliable data consistency.

---

# ⭐ Key Capabilities

## 1. Full T-SQL Support

Supports familiar SQL Server syntax, including:

- DDL
- DML
- MERGE (Upsert operations)

---

## 2. Fully Managed

Microsoft automatically manages:

- Infrastructure
- Compute scaling
- Storage

No server administration is required.

---

## 3. OneLake Integration

Warehouse data is stored once and shared across Fabric workloads.

Benefits include:

- No duplicate datasets
- Unified storage
- Simplified analytics

---

## 4. Cross-Database Querying

Query data across:

- Warehouses
- Lakehouses

without copying data.

### Three-Part Naming

```text
database.schema.table
```

Example:

```text
SalesWarehouse.dbo.FactSales
```

---

## 5. Familiar SQL Tools

Supported clients include:

- SQL Server Management Studio (SSMS)
- Azure Data Studio
- Other TDS-compatible SQL clients

---

## 6. Copilot Assistance

Copilot can:

- Generate SQL queries
- Autocomplete SQL
- Explain existing code
- Suggest query fixes

---

# ⚖️ Warehouse vs SQL Analytics Endpoint

| Capability | Warehouse | SQL Analytics Endpoint |
|------------|-----------|------------------------|
| Read Data | ✅ Yes | ✅ Yes |
| Insert Data | ✅ Yes | ❌ No |
| Update Data | ✅ Yes | ❌ No |
| Delete Data | ✅ Yes | ❌ No |
| MERGE Support | ✅ Yes | ❌ No |
| Create Tables | ✅ Yes | ❌ No |
| Create Views | ✅ Yes | ✅ Yes |
| Create Stored Procedures | ✅ Yes | ✅ Yes |
| Data Source | Native Warehouse Tables | Lakehouse Delta Tables |

### Use a Warehouse when:

- You need full read/write SQL capabilities.
- You need transactional workloads.
- You need to build relational warehouse tables.

### Use the SQL Analytics Endpoint when:

- You only need read-only SQL access to Lakehouse data.

---

# 🏗️ Create a Data Warehouse

A Data Warehouse can be created from:

- Fabric Create Hub
- Fabric Workspace

Once created, you can begin creating:

- Tables
- Views
- Stored Procedures

using the SQL Query Editor.

---

# 📥 Ingest Data into a Warehouse

Microsoft Fabric provides several ingestion methods.

---

## 1. COPY INTO

Bulk loads files into Warehouse tables.

### Supported Formats

- CSV
- Parquet

### Best For

- Large data imports
- Batch loading

---

## 2. OPENROWSET

Reads files directly without importing them first.

### Uses

- Ad-hoc analysis
- External file querying
- Data validation

---

## 3. Pipelines and Dataflows

Use:

- Data Factory Pipelines
- Dataflows Gen2

to automate ETL processes.

---

## 4. Cross-Database Queries

Query Lakehouse tables directly from the Warehouse.

### Benefits

- No data duplication
- Live access to Lakehouse data
- Simplified integration

---

# 🗄️ Create Tables

Tables are created using **CREATE TABLE** statements.

Example objects include:

### Dimension Tables

- DimCustomer
- DimProduct
- DimDate

### Fact Tables

- FactSales

---

# 📌 Choosing Data Types

Use appropriate data types for performance and storage efficiency.

| Data Type | Typical Use |
|------------|-------------|
| `INT` | Keys and numeric identifiers |
| `NVARCHAR` | Text with Unicode support |
| `DECIMAL` | Financial and precise numeric values |

---

# 🚧 Staging Tables

## What are Staging Tables?

Staging Tables temporarily store raw source data before it is transformed into Fact and Dimension Tables.

---

## Typical Workflow

```text
Source Data
      ↓
COPY INTO / Pipeline
      ↓
Staging Tables
      ↓
Business Rules
      ↓
Dimension Tables
      ↓
Fact Tables
```

---

## Benefits

- Preserves original data
- Simplifies transformations
- Enables key lookups
- Supports data validation

---

# 🔄 Data Transformation

After loading staging tables:

1. Join staging data with dimensions.
2. Perform key lookups.
3. Apply business rules.
4. Insert cleaned data into Fact Tables.

This creates a well-structured dimensional model for analytics.

---

# 📑 Table Clones

## What are Table Clones?

A **Table Clone** creates a metadata-only copy of an existing table.

The cloned table references the same underlying data stored in OneLake.

No data is physically duplicated.

---

## Benefits

- Minimal storage usage
- Fast creation
- Zero-copy architecture

---

## Common Use Cases

- Development
- Testing
- Backup before deployments
- Historical snapshots
- Data recovery

---

# 🔄 End-to-End Warehouse Workflow

```text
Source Systems
        ↓
COPY INTO / Pipelines
        ↓
Staging Tables
        ↓
Transformations
        ↓
Dimension Tables
        ↓
Fact Tables
        ↓
SQL Queries
        ↓
Power BI
        ↓
Copilot & AI
```

---

# 📝 Key Takeaways

- A **Microsoft Fabric Data Warehouse** is a fully managed relational database built on **OneLake**.
- It supports full transactional **T-SQL**, including DDL and DML operations.
- Warehouse data is stored in **Delta format**, enabling seamless integration with other Fabric workloads.
- Cross-database queries allow Warehouses and Lakehouses to work together without copying data.
- Data can be ingested using **COPY INTO**, **OPENROWSET**, **Pipelines**, or **Cross-Database Queries**.
- **Staging Tables** provide a temporary landing area before loading Fact and Dimension tables.
- **Table Clones** create metadata-only copies that share the same underlying data, reducing storage costs.
- Copilot assists with SQL generation, code completion, and query optimization.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| Fabric Data Warehouse | Fully managed relational database for analytics |
| OneLake | Unified storage layer for Microsoft Fabric |
| Delta Format | Open storage format used by Fabric Warehouses |
| DDL (Data Definition Language) | SQL commands used to define database objects (CREATE, ALTER, DROP) |
| DML (Data Manipulation Language) | SQL commands used to modify data (INSERT, UPDATE, DELETE, MERGE) |
| ACID Transactions | Ensures reliable and consistent database operations |
| COPY INTO | Bulk-load command for importing files into Warehouse tables |
| OPENROWSET | Reads external files without importing them |
| Cross-Database Query | Queries data across Warehouses and Lakehouses without copying it |
| Three-Part Naming | Database reference format: `database.schema.table` |
| Staging Table | Temporary table used before loading Fact and Dimension tables |
| Table Clone | Metadata-only copy that shares the same underlying OneLake data |
| Copilot | AI assistant for generating, explaining, and optimizing SQL queries |
