# 📘 Browse and Connect to Data in OneLake

## 🎯 Overview

The **OneLake Catalog** is Microsoft Fabric's centralized data discovery experience, allowing users to find, understand, and connect to data across the organization.

Instead of creating duplicate datasets, users can discover existing assets, connect to them using **Shortcuts**, and reuse trusted semantic models for analytics and reporting.

---

# 🔍 Find Data in the OneLake Catalog

## What is the OneLake Catalog?

The **OneLake Catalog** is a searchable inventory of all Microsoft Fabric data assets within a tenant.

It enables users to:

- Search data by name or tag
- Browse organizational data
- Discover trusted datasets
- Reuse existing data assets
- Reduce data duplication

---

## Permission-Based Discovery

The OneLake Catalog respects security permissions.

### Benefits

- Users only see data they are authorized to access.
- Sensitive data remains protected.
- Supports secure collaboration across teams.

---

## Metadata Available

Each catalog item provides useful metadata to help determine whether it is suitable for use.

### Metadata Includes

- Name
- Item type
- Owner
- Last refresh time
- Workspace location
- Sensitivity labels
- Endorsement status

---

# 🔒 Sensitivity Labels

Sensitivity labels help classify and protect organizational data.

### Purpose

- Identify sensitive information
- Support governance
- Guide access decisions
- Improve compliance

---

# ⭐ Endorsement Levels

Endorsements help users identify trusted data assets.

| Level | Description |
|--------|-------------|
| **Promoted** | Ready for sharing; any user with write permission can promote it. |
| **Certified** | Meets organizational quality standards; only authorized reviewers can certify it. |
| **Master Data** | Official source of truth for core business data (e.g., customers or products); only authorized reviewers can assign this label. |

> **Note:** All Fabric and Power BI items (except dashboards) can be **Promoted** or **Certified**. The **Master Data** label applies only to data items such as lakehouses and semantic models.

---

# 🔗 Connect to Data Using Shortcuts

## What are Shortcuts?

**Shortcuts** allow you to reference data stored in another workspace or external location **without copying or moving it**.

Any changes made to the source data are immediately reflected in the shortcut.

---

## Benefits of Shortcuts

- No data duplication
- Always uses the latest source data
- Supports cross-workspace collaboration
- Enables data reuse
- Reduces storage costs
- Supports Medallion Architecture

---

## Example Use Case

A data engineering team maintains cleaned transaction tables in a lakehouse.

An analytics team can:

1. Create a shortcut to the engineering lakehouse.
2. Build business-ready datasets.
3. Add calculated columns.
4. Create fact and dimension tables.
5. Aggregate data for reporting.

No data needs to be copied.

---

# 🏅 Medallion Architecture Support

Shortcuts support the **Medallion Architecture**, where data is organized into layers.

### Layers

- **Bronze** → Raw data
- **Silver** → Cleaned and enriched data
- **Gold** → Curated business-ready data

---

# 🗄️ SQL Analytics Endpoint

Every Lakehouse includes a **SQL Analytics Endpoint**.

## Purpose

Provides read-only **T-SQL** access to Lakehouse tables.

### Common Uses

- Preview data
- Validate schemas
- Explore tables
- Run SQL queries before creating shortcuts

---

## Copilot Integration

Copilot can help write:

- T-SQL queries
- Data exploration queries
- Validation queries

This is the same mechanism AI agents use to query Lakehouse data.

---

# 🛠️ Create a Shortcut

## Steps

1. Open your Lakehouse.
2. Select **New Shortcut**.
3. Choose **OneLake** as the source.
4. Browse to the desired workspace and Lakehouse.
5. Select the required tables or folders.
6. Confirm the shortcut creation.

Once created, the shortcut behaves like a normal table.

---

## Working with Shortcuts

Shortcuts can be accessed using:

- SQL Queries
- Notebooks
- Dataflows

Common tasks include:

- Creating fact tables
- Creating dimension tables
- Adding calculated columns
- Aggregating data
- Data transformation

---

## When Not to Use Shortcuts

Shortcuts may not be suitable when:

- A fixed snapshot of data is required.
- Network latency affects performance.
- Compliance requires physically separate copies of the data.

---

# 📊 Work with Semantic Models

## What are Semantic Models?

Semantic Models are business-ready datasets that include:

- Relationships
- Calculations
- Measures
- Business metrics

They simplify report creation by providing a curated data model.

---

# 🔍 Explore a Semantic Model

Select a semantic model in the OneLake Catalog and choose **Open**.

---

## Overview Tab

Displays:

- Description
- Owner
- Refresh status
- Endorsement level
- Sensitivity labels

---

## Tables Section

Shows:

- Tables
- Columns
- Schema

Users can inspect sample data using the **Binoculars** icon.

---

## Lineage Tab

Displays:

- Upstream dependencies
- Downstream dependencies
- Data flow relationships

---

## Monitor Tab

Shows:

- Refresh history
- Activity logs
- Processing status

---

# 📈 Create Reports from Semantic Models

Once you've confirmed the semantic model contains the required data, you can create reports using **Explore this data**.

## Available Options

### Explore This Data

- Perform quick ad-hoc analysis
- Matrix visualizations

---

### Auto-Create Report

Automatically generates:

- Visualizations
- Summary insights
- Basic report layout

---

### Create Blank Report

Opens the Power BI report editor for building a custom report.

---

### Create from Template

Creates a report using an existing report template.

---

### Create Paginated Report

Generates formatted reports suitable for:

- Printing
- PDF export
- Operational reporting

---

# 📊 Analyze in Excel

Semantic models can also be connected directly to **Microsoft Excel**.

### Benefits

- Create PivotTables
- Familiar Excel interface
- Interactive analysis
- Reuse trusted business data

---

# 📝 Key Takeaways

- The **OneLake Catalog** is the central hub for discovering Microsoft Fabric data assets.
- Users can search data by name, tag, workspace, or metadata.
- Permission-based visibility ensures secure access to data.
- Metadata, sensitivity labels, and endorsements help identify trusted datasets.
- **Shortcuts** allow access to data without copying or duplicating it.
- SQL Analytics Endpoints provide read-only T-SQL access to Lakehouse tables.
- Copilot assists with writing SQL queries for data exploration.
- Semantic Models provide business-ready datasets with predefined relationships and calculations.
- Reports can be created directly from semantic models or analyzed in Microsoft Excel.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| OneLake Catalog | Centralized discovery portal for Microsoft Fabric data assets |
| Metadata | Information describing a data asset (owner, refresh time, labels, etc.) |
| Sensitivity Label | Classification used to protect sensitive organizational data |
| Promoted | Data asset approved for sharing |
| Certified | Data asset verified to meet organizational quality standards |
| Master Data | Official source of truth for core organizational data |
| Shortcut | Reference to data without copying or moving it |
| SQL Analytics Endpoint | Read-only T-SQL interface for querying Lakehouse tables |
| Semantic Model | Business-ready dataset containing relationships, measures, and calculations |
| Lineage | Visualization of upstream and downstream data dependencies |
| Medallion Architecture | Data organization approach using Bronze, Silver, and Gold layers |
| Direct Query | Live access to data without importing it into another dataset |
```
