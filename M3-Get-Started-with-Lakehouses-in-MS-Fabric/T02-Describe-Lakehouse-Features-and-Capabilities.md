# 📘 Describe Lakehouse Features and Capabilities

## 🎯 Overview

Traditional analytics solutions often require choosing between:

- **Data Lakes** → Flexible and scalable but limited for analytics.
- **Data Warehouses** → Powerful for analytics but less flexible and expensive to scale.

A **Lakehouse** combines the strengths of both, enabling organizations to store, process, and analyze all types of data in a single platform.

---

# 🏗️ Lakehouse Design

A Lakehouse organizes data into two main areas:

- **Tables**
- **Files**

This separation supports both raw data storage and optimized analytics.

---

# 📊 Tables Folder

The **Tables** folder stores **Delta Lake tables**, which contain structured and queryable data.

## Features

- Supports SQL queries through the **SQL Analytics Endpoint**
- Enforces schemas
- Supports **ACID transactions**
- Accessible from Power BI
- Automatically optimized and maintained

### Best For

- Business analytics
- Reporting
- Dashboards
- Structured datasets

---

# 📁 Files Folder

The **Files** folder stores raw or semi-structured data in its original format.

## Supported Formats

- CSV
- JSON
- Parquet
- Images
- Documents
- Other file formats

## Features

- Stores data in native format
- Supports data staging before transformation
- Flexible for exploration and processing
- No enforced schema
- Cannot be queried directly with SQL

### Best For

- Raw data storage
- Data ingestion
- Compliance
- Reprocessing

---

# 🔄 Typical Lakehouse Workflow

A common workflow involves:

1. Load raw files into the **Files** folder.
2. Process and clean the data using:
   - Spark Notebooks
   - Dataflows Gen2
3. Store transformed data as **Delta Tables**.
4. Query data using SQL.
5. Build reports and dashboards in Power BI.

---

# 🗄️ Delta Lake Tables

## What is Delta Lake?

**Delta Lake** is an open-source storage layer that adds database-like capabilities to data lakes.

When tables are created in a Lakehouse, they are stored as **Delta Tables** in OneLake.

---

## Delta Lake Features

### 🔒 ACID Transactions

Ensures reliable data operations even when multiple users read and write simultaneously.

**Benefits**

- Data consistency
- Reliable concurrent access

---

### ✅ Schema Enforcement

Ensures incoming data matches the table schema.

**Benefits**

- Prevents invalid data
- Maintains data quality

---

### ⏳ Time Travel

Maintains a transaction log of every change.

Allows users to:

- Query previous versions
- Restore earlier data
- Roll back unwanted changes

---

### ✏️ Efficient Updates and Deletes

Unlike traditional data lake files, Delta Tables support efficient:

- UPDATE
- DELETE
- MERGE

operations without rewriting the entire dataset.

---

## Delta Table Architecture

Each Delta Table consists of:

- **Parquet Data Files**
- **Transaction Log**

The transaction log tracks all changes and enables reliable batch and streaming workloads.

---

# 🔐 Lakehouse Security and Access Management

Microsoft Fabric provides multiple layers of security.

---

## Workspace Roles

Use workspace roles when users need access to all workspace items.

Typical roles include:

- Admin
- Member
- Contributor
- Viewer

---

## Item-Level Sharing

Allows read-only access to specific assets without granting access to the entire workspace.

Ideal for:

- Analysts
- Report developers
- Business users

---

## SQL Analytics Endpoint Security

Supports fine-grained access control.

### Row-Level Security (RLS)

Restricts which rows users can view.

---

### Column-Level Security (CLS)

Restricts access to sensitive columns.

---

### Schema-Level Permissions

When tables are organized into schemas, permissions can be granted by business domain.

---

# 🛡️ Governance

Fabric supports enterprise governance features.

## Features

- Sensitivity Labels
- Data Classification
- Access Control
- Microsoft Purview Integration

### Benefits

- Improved compliance
- Better security
- Centralized governance

---

# 🤖 Lakehouses and Intelligent Analytics

Well-designed Lakehouse data supports more than traditional analytics.

It also enables AI-powered experiences across Microsoft Fabric.

---

## Best Practices

Create tables with:

- Clear schemas
- Consistent naming conventions
- Descriptive column names
- Well-documented metadata

These practices improve usability for both humans and AI.

---

# 🧠 Fabric IQ and AI Agents

Fabric IQ Data Agents use the **SQL Analytics Endpoint** to:

- Translate natural language into SQL
- Query Lakehouse tables
- Return accurate answers

The quality of AI responses depends on how well the data is organized.

---

# 🤖 Copilot Integration

Copilot benefits from structured Lakehouse data by enabling:

- Automatic report generation
- Natural language querying
- Business insight generation
- Data exploration

Lakehouse tables can also serve as the foundation for **Power BI Semantic Models**.

---

# 🌐 Benefits Across Microsoft Fabric

Well-structured Lakehouse data supports:

- Power BI Reports
- Semantic Models
- Fabric IQ
- Copilot
- Microsoft 365 AI Experiences
- Business Intelligence
- Self-service Analytics

---

# 📝 Key Takeaways

- A Lakehouse combines the flexibility of a Data Lake with the analytical power of a Data Warehouse.
- Data is organized into **Tables** and **Files** folders.
- Delta Lake provides ACID transactions, schema enforcement, time travel, and efficient updates.
- Raw files are processed into Delta Tables for analytics.
- SQL Analytics Endpoints provide secure SQL access to Lakehouse tables.
- Microsoft Fabric supports layered security through workspace roles, item sharing, RLS, CLS, and schema permissions.
- Microsoft Purview enhances governance with sensitivity labels and data classification.
- Well-structured Lakehouse data improves analytics and enables AI capabilities such as Fabric IQ and Copilot.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| Lakehouse | Unified platform combining Data Lake storage and Data Warehouse analytics |
| Tables Folder | Stores structured Delta Lake tables for analytics |
| Files Folder | Stores raw and semi-structured files in native formats |
| Delta Lake | Open-source storage layer that adds reliability to data lakes |
| Delta Table | Table stored as Parquet files with a transaction log |
| Parquet | Open columnar storage format used for analytics |
| Transaction Log | Records all changes made to Delta Tables |
| ACID Transactions | Ensures reliable and consistent database operations |
| Schema Enforcement | Validates incoming data against the table schema |
| Time Travel | Ability to query or restore previous versions of data |
| SQL Analytics Endpoint | Read-only SQL interface for querying Lakehouse tables |
| Row-Level Security (RLS) | Restricts access to specific rows of data |
| Column-Level Security (CLS) | Restricts access to specific columns of data |
| Schema-Level Permissions | Controls access based on database schemas |
| Microsoft Purview | Data governance and compliance platform |
| Fabric IQ | AI capability that queries governed Lakehouse data |
| Copilot | AI assistant that generates insights and reports from structured data |
