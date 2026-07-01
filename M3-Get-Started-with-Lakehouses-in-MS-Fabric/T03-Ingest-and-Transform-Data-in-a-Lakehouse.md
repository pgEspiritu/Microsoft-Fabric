# 📘 Ingest and Transform Data in a Lakehouse

## 🎯 Overview

Before a **Lakehouse** can provide insights, it must first ingest and transform data.

Microsoft Fabric provides multiple no-code and code-based methods to:

- Import data
- Transform data
- Load data into Delta Lake tables
- Prepare data for analytics and AI

---

# 🏗️ Create and Explore a Lakehouse

A Lakehouse is created within a **Fabric-enabled Workspace**.

Every Lakehouse contains:

- **Tables**
- **Files**
- **SQL Analytics Endpoint**

---

# 📊 Tables

The **Tables** area stores **Delta Lake Tables**.

## Features

- Structured data
- SQL query support
- Schema enforcement
- ACID transactions
- Power BI integration
- Queryable through SQL Analytics Endpoint

### Best For

- Analytics
- Reporting
- Business intelligence

---

# 📁 Files

The **Files** area stores raw and semi-structured data.

## Supported Formats

- CSV
- JSON
- Parquet
- Other file formats

### Features

- Native file storage
- Flexible staging area
- No enforced schema
- Ideal before transformation

---

# 🗂️ Schemas

Schemas are enabled automatically when a Lakehouse is created.

## Default Schema

- **dbo**

---

## Purpose of Schemas

Schemas organize tables into logical business domains.

### Example Schemas

- sales
- marketing
- hr
- finance

---

## Benefits

- Better organization
- Easier data discovery
- Schema-level permissions
- Cross-workspace queries
- Improved AI discoverability

---

## Four-Part Namespace

Schema-enabled Lakehouses support cross-workspace querying using:

```text
workspace.lakehouse.schema.table
```

Example:

```text
SalesWorkspace.SalesLakehouse.sales.Customers
```

---

# 🤖 AI Benefit

Well-organized schemas improve discoverability for:

- Fabric IQ
- Copilot
- AI Data Agents

These AI tools translate natural language into SQL queries more accurately when tables are well organized.

---

# 🖥️ Lakehouse Working Modes

There are two ways to work with a Lakehouse.

---

## 1. Lakehouse Explorer

Used for:

- Uploading files
- Managing folders
- Creating tables
- Viewing data
- Managing multiple Lakehouses

### Features

- Upload local files
- Create tables
- Browse folders
- Add reference Lakehouses

---

## 2. SQL Analytics Endpoint

Provides read-only **T-SQL** access to Delta Tables.

### Supports

- SQL Queries
- Views
- Functions
- Security

### Does Not Support

- Modifying table data

---

# 📥 Ingest Data into a Lakehouse

Data ingestion is the first stage of the **ETL (Extract, Transform, Load)** process.

Microsoft Fabric provides several ingestion methods.

---

## 1. Upload

Upload files or folders directly through the Lakehouse Explorer.

### Best For

- Small datasets
- Local files
- Quick testing

---

## 2. Load to Table

A no-code feature that converts supported files directly into Delta Tables.

### Supported Formats

- CSV
- Parquet

### Options

- Create new table
- Append existing data
- Overwrite existing table

---

## 3. Dataflows Gen2

Uses **Power Query** to:

- Import data
- Clean data
- Transform data

Ideal for users familiar with:

- Excel
- Power BI

---

## 4. Notebooks

Use **Apache Spark** to programmatically:

- Load data
- Transform data
- Create Delta Tables

Supported languages include:

- PySpark
- SQL
- Scala

---

## 5. Data Factory Pipelines

Use **Copy Data** activities to move data from external sources into OneLake.

### Benefits

- Automated ETL
- Scheduled execution
- Integration with many data sources

---

# 📊 Data Loading Strategies

Two common approaches are used.

---

## Option 1: Stage Raw Data

```text
Source Data
      ↓
Files
      ↓
Transform
      ↓
Delta Tables
```

### Benefits

- Preserve original data
- Support reprocessing
- Better auditing

---

## Option 2: Load Directly into Tables

```text
Source Data
      ↓
Delta Tables
```

### Best When

- Data is already clean
- Data is in supported formats
- Minimal transformation is required

---

# 🔗 Access Data Using Shortcuts

## What are Shortcuts?

Shortcuts reference external data without copying it into the Lakehouse.

The referenced data appears as though it exists locally.

---

## Benefits

- No data duplication
- Reduced storage costs
- Shared access
- Always uses current source data

---

## Supported Sources

- Another OneLake location
- Azure Data Lake Storage Gen2
- Other cloud storage
- Other Microsoft Fabric items

---

## Permissions

Access through Shortcuts uses your own identity.

Users must already have permission to access the source data.

---

# 🗂️ Schema Shortcuts

Schema Shortcuts map an entire schema from another Lakehouse or ADLS Gen2.

### Benefits

- Entire schemas become available locally
- Referenced tables appear like native Lakehouse tables
- Simplifies cross-workspace collaboration

---

# 🔄 Transform Data in a Lakehouse

Raw data typically requires transformation before analysis.

Common workflow:

```text
Raw Files
      ↓
Transformation
      ↓
Delta Tables
      ↓
Analytics
```

---

# 🧑‍💻 Transformation Tools

## Notebooks

Preferred by data engineers.

### Languages

- PySpark
- SQL
- Scala

### Uses

- Data cleansing
- Data transformation
- Machine learning
- Automation

### Copilot Features

- Generate Spark code
- Explain existing code
- Assist with transformations

---

## Dataflows Gen2

Uses **Power Query**.

Ideal for:

- Business analysts
- Excel users
- Power BI users

Provides a low-code interface for ETL.

---

## Pipelines

Provide a visual workflow designer.

### Capabilities

- Multiple ETL activities
- Sequential execution
- Parallel execution
- Automated orchestration

---

# 🔄 Typical ETL Workflow

```text
External Data
        ↓
Upload / Pipeline / Shortcut
        ↓
Files
        ↓
Dataflow Gen2 / Notebook
        ↓
Delta Tables
        ↓
SQL Analytics Endpoint
        ↓
Power BI / Copilot / Fabric IQ
```

---

# 📝 Key Takeaways

- Every Lakehouse contains **Tables**, **Files**, and a **SQL Analytics Endpoint**.
- Schemas organize Lakehouse tables into logical business domains.
- Fabric supports multiple ingestion methods, including Upload, Load to Table, Dataflows Gen2, Notebooks, and Pipelines.
- Shortcuts provide access to external data without copying it.
- Schema Shortcuts expose entire schemas from external Lakehouses.
- Data transformations can be performed using Notebooks, Dataflows Gen2, or Pipelines.
- Copilot assists with Spark code generation and SQL development.
- Well-organized Lakehouses improve analytics, governance, and AI capabilities.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| Lakehouse Explorer | Interface for managing files, folders, and tables |
| SQL Analytics Endpoint | Read-only T-SQL interface for querying Delta Tables |
| Schema | Logical grouping of related tables |
| dbo | Default schema created with every Lakehouse |
| ETL | Extract, Transform, Load process |
| Upload | Manual file ingestion into a Lakehouse |
| Load to Table | No-code feature that creates Delta Tables from files |
| Dataflows Gen2 | Power Query-based ETL tool |
| Notebook | Apache Spark development environment |
| Pipeline | Visual workflow for orchestrating ETL |
| Shortcut | Reference to external data without copying it |
| Schema Shortcut | Shortcut exposing an entire external schema as local tables |
| PySpark | Python API for Apache Spark |
| Scala | Programming language commonly used with Spark |
| Delta Table | Structured table stored in Delta Lake format |
