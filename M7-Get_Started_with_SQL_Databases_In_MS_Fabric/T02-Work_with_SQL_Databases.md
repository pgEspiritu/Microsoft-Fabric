# Work with SQL Databases in Microsoft Fabric

## Overview

**SQL Database in Microsoft Fabric** is a **Software as a Service (SaaS)** transactional database built on **Azure SQL Database**. It enables developers and organizations to create, manage, and query operational databases while integrating seamlessly with the Microsoft Fabric ecosystem.

Unlike **Azure SQL Database (PaaS)**, SQL Database in Fabric is fully managed as a **SaaS** solution, reducing administrative overhead.

One of its key capabilities is the **automatic replication of data into OneLake** and conversion to **Parquet** format in near real-time, eliminating the need for complex ETL processes.

---

# Key Features

- Built on Azure SQL Database.
- Fully managed **Software as a Service (SaaS)**.
- Supports operational (transactional) databases.
- Automatically replicates data to **OneLake**.
- Converts replicated data to **Parquet** format.
- Near real-time synchronization.
- Native integration with Microsoft Fabric services.

---

# Benefits

- Minimal database maintenance.
- Simplified operational database management.
- No complex ETL required for analytics.
- Near real-time analytical data availability.
- Unified platform for operational and analytical workloads.

---

# Fabric Integration

Replicated data stored in **OneLake** can be accessed directly by:

- Spark
- Notebooks
- Power BI
- Other Microsoft Fabric workloads

This enables analytics without copying or manually transforming data.

---

# Create a SQL Database

To create a new SQL Database:

1. Open the **Microsoft Fabric** portal.
2. Navigate to **Databases**.
3. Select **New → SQL Database**.
4. Enter a database name.
5. Select **Create**.

After provisioning, the **Explorer** pane displays all database objects.

---

# Build Your Database

A newly created database provides three quick-start options:

### Sample Data

- Import the **AdventureWorksLT** sample database.

### T-SQL Editor

- Create:
  - Schemas
  - Tables
  - Views
  - Other database objects

### Connection Strings

Provides connection information for tools such as:

- SQL Server Management Studio (SSMS)
- Visual Studio Code
- Other SQL clients

---

# Query a SQL Database

SQL Database in Fabric supports standard SQL tools.

Available options include:

- Built-in web-based SQL Editor
- SQL Server Management Studio (SSMS)
- Visual Studio Code (VS Code)

The **Open in** option automatically pre-fills connection details for supported tools.

---

# Source Control Integration

SQL Database supports source control for database development.

## Commit to Source Control

- Save database objects as code.
- Export schemas, tables, views, procedures, and other objects.
- Store changes in a repository.

## Update from Source Control

- Apply validated changes from the repository.
- Uses differential updates instead of recreating objects.

## History Tracking

- View modification history.
- Track changes.
- Improve collaboration.
- Restore previous versions when necessary.

---

# Performance Monitoring

## Performance Dashboard

The **Performance Dashboard** provides database monitoring and performance insights.

It supports users with different experience levels:

### Beginner

- Basic query performance metrics

### Intermediate

- Detailed workload information

### Advanced

- Comprehensive performance diagnostics

Access the dashboard by:

- Selecting the **three-dot menu** on the database item → **Open performance summary**
- Opening the **Query Editor** → **Performance summary**

---

# Performance Dashboard Features

- Query performance monitoring
- Database health metrics
- Performance alerts
- Bottleneck detection
- Query optimization insights

---

# Automatic Tuning

SQL Database in Fabric includes **Automatic Tuning**, which uses **Machine Learning** to improve database performance.

Capabilities include:

- Detects inefficient queries
- Creates recommended indexes
- Removes unused indexes
- Reverts ineffective changes automatically

---

# Automatic Index Management

The **Automatic Index** tab displays:

- Created indexes
- Dropped indexes
- Reverted indexes
- Schema name
- Table name
- Index name
- Status
- Key columns
- Included columns
- Creation date
- Drop date

---

# Key Takeaways

- SQL Database in Fabric is a **SaaS** transactional database built on **Azure SQL Database**.
- Automatically replicates operational data to **OneLake** in **Parquet** format.
- Supports SQL querying through the web editor, SSMS, and Visual Studio Code.
- Integrates with source control for version management and collaboration.
- Includes a **Performance Dashboard** for monitoring database health.
- Uses **Automatic Tuning** and **Automatic Indexing** to optimize query performance with minimal manual effort.
