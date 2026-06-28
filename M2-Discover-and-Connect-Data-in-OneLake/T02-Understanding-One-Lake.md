# 📘 Understand OneLake

## 🎯 Overview

**OneLake** is the foundation of Microsoft Fabric's analytics platform. It provides a **single, unified storage layer** where all organizational data is stored and shared across every Fabric workload.

Unlike traditional analytics environments, OneLake eliminates the need to copy data between systems or manage multiple storage accounts by providing one centralized storage location.

---

# 🌊 OneLake is Tenant-Wide

## What is Tenant-Wide?

OneLake is automatically available for every Microsoft Fabric tenant.

### Key Features

- Automatically created when Fabric is enabled
- No additional setup or configuration required
- Shared across the entire organization
- Accessible by all Fabric workloads

### Benefits

- Single copy of data
- Eliminates data silos
- Reduces storage costs
- Provides a single source of truth
- Ensures everyone works with the latest data

---

# 🔄 Single Source of Truth

Traditional analytics environments often maintain multiple copies of the same data for different teams.

With OneLake:

- All workloads read from the same underlying files.
- Updates become immediately available to all users.
- No duplicate datasets are required.
- Data consistency is maintained across the organization.

### Advantages

- Reduced data duplication
- Lower storage costs
- Improved collaboration
- Consistent analytics results

---

# 🔍 Discover Data with the OneLake Catalog

## What is the OneLake Catalog?

The **OneLake Catalog** is a searchable inventory of all data assets stored in OneLake.

It helps users quickly discover and understand available organizational data.

---

## Catalog Features

### Search and Browse

Users can:

- Search assets by name
- Browse by workspace
- Browse by business domain

### Metadata

The catalog displays:

- Asset descriptions
- Owners
- Data lineage
- Additional metadata

### Benefits

- Faster data discovery
- Easier collaboration
- Improved data understanding

---

# 🔒 Governance and Security

OneLake integrates with **Microsoft Purview** to provide enterprise-grade governance.

## Governance Features

- Data classification
- Sensitivity labels
- Data lineage tracking
- Access control
- Security management

### Benefits

- Improved compliance
- Better data protection
- Controlled access to sensitive information

---

# 📂 Types of Data Stored in OneLake

OneLake stores data using **open formats**, ensuring compatibility with multiple analytics tools.

## Default Table Format

- **Delta Lake**

Delta Lake stores data as:

- Open **Parquet** files

Any tool supporting Delta Lake or Parquet can access the data.

---

## Supported Data Types

### Tables

Stored in:

- Lakehouses
- Warehouses
- Eventhouses

---

### Files

Supported formats include:

- Parquet
- CSV
- JSON
- Other file formats

---

### Shortcuts

References to external data without copying it.

Supported locations include:

- Azure Data Lake Storage (ADLS)
- Amazon S3
- Another OneLake location

### Benefits

- No data duplication
- Data remains in its original location
- Easier governance
- Shared access across teams

---

### Semantic Models

Used by Power BI for:

- Business reporting
- Data analysis
- Interactive dashboards

---

# 📥 How Data Arrives in OneLake

OneLake supports multiple ingestion methods.

---

## 1. Mirroring

Continuously replicates data from external databases.

### Supported Sources

- SQL Server
- Azure SQL Database
- Azure Cosmos DB
- Snowflake

### Benefits

- Automatic synchronization
- Near real-time updates

---

## 2. Pipelines

Automate data movement and transformation using Data Factory capabilities.

### Functions

- Copy data
- Transform data
- Load data into OneLake

---

## 3. Dataflows

Built with **Power Query**.

### Functions

- Connect to data sources
- Transform data
- Load data into OneLake

Ideal for users familiar with:

- Excel
- Power BI

---

## 4. Streaming

Supports continuous ingestion of real-time data using **Eventstreams**.

### Common Sources

- IoT devices
- Application logs
- Clickstream data

---

## 5. Direct Upload

Users can upload files directly into OneLake through the Microsoft Fabric interface.

---

# 🤖 OneLake and AI

OneLake provides the foundation for AI capabilities in Microsoft Fabric.

## AI Features

- Copilot
- Fabric IQ
- AI Agents

These services use the **OneLake Catalog** to discover and understand organizational data.

---

## Example

When you ask Copilot:

> "What were last quarter's sales trends?"

Copilot:

1. Searches the OneLake Catalog.
2. Finds relevant datasets.
3. Understands metadata and relationships.
4. Generates accurate responses.

---

## Importance of Well-Governed Data

AI performs better when data is:

- Well organized
- Properly named
- Clearly described
- Rich in metadata
- Easy to discover

Good governance directly improves AI-generated insights.

---

# 📝 Key Takeaways

- OneLake is the centralized storage layer of Microsoft Fabric.
- It is automatically available across the entire Fabric tenant.
- OneLake provides a single source of truth by eliminating duplicate datasets.
- The OneLake Catalog helps users discover, browse, and understand organizational data.
- OneLake integrates with Microsoft Purview for governance and security.
- Data is stored in open formats such as Delta Lake and Parquet.
- OneLake supports multiple ingestion methods including Mirroring, Pipelines, Dataflows, Streaming, and Direct Upload.
- Shortcuts allow access to external data without copying it.
- Copilot and Fabric IQ rely on the OneLake Catalog to discover governed data and provide AI-powered insights.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| OneLake | Unified, tenant-wide storage layer for Microsoft Fabric |
| OneLake Catalog | Searchable inventory of organizational data assets |
| Microsoft Purview | Data governance and security platform |
| Delta Lake | Default open table format used by OneLake |
| Parquet | Open columnar file format used for analytics |
| Shortcut | Reference to external data without copying it |
| Lakehouse | Storage and analytics environment in Fabric |
| Warehouse | Structured analytical data repository |
| Eventhouse | Storage optimized for streaming and event data |
| Semantic Model | Business-friendly data model used by Power BI |
| Mirroring | Continuous replication of external databases into OneLake |
| Pipeline | Automated data ingestion and transformation workflow |
| Dataflow | Low-code ETL tool built with Power Query |
| Eventstream | Real-time streaming data ingestion service |
| Copilot | AI assistant powered by OneLake data |
| Fabric IQ | AI capability that uses OneLake metadata and governance |
