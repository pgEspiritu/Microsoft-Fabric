# Simplify Data Management with Mirroring and Data Virtualization

## Overview

Microsoft Fabric simplifies data integration through **Database Mirroring** and **Data Virtualization**.

These capabilities help organizations:

- Integrate data from multiple sources.
- Maintain near real-time data availability.
- Eliminate complex ETL processes.
- Analyze data without duplicating or moving it.

---

# Database Mirroring

## What is Mirroring?

**Database Mirroring** continuously replicates data from **Azure SQL Database** into **Microsoft Fabric OneLake**.

Additionally, **SQL Database in Fabric** is automatically mirrored into OneLake for analytics.

Replication occurs in **near real-time**, making fresh operational data immediately available for analytical workloads.

---

# Benefits of Mirroring

- Near real-time data synchronization
- Eliminates complex ETL pipelines
- Reduces total cost of ownership (TCO)
- Accelerates time-to-insight
- Keeps analytical data continuously updated

Supports workloads such as:

- Business Intelligence (BI)
- Artificial Intelligence (AI)
- Data Engineering
- Data Science
- Data Sharing

---

# Monitor Replication

After starting a mirroring process, replication status can be monitored.

**Navigation:**

**Replication Tab → Monitor Replication**

Monitoring allows you to:

- View replication status
- Check synchronization progress
- Detect replication issues

If no source data changes occur, the replication engine reduces polling frequency and resumes normal polling once updates are detected.

---

# Data Virtualization

## What is Data Virtualization?

**Data Virtualization** allows SQL Database in Fabric to access external data **without physically copying or moving it**.

Instead of importing data, SQL queries reference external storage directly.

This provides a unified view across multiple data sources.

---

# Benefits of Data Virtualization

- No data duplication
- Reduced storage requirements
- Access multiple data sources from one database
- Simplified data integration
- Faster analytics across platforms

---

# Supported External Data

SQL Database in Fabric can query data stored in:

- Parquet files
- CSV files
- Delta tables
- Microsoft OneLake

---

# Data Virtualization Components

## Database Scoped Credential

Provides secure authentication for external data sources.

Example:

```sql
CREATE DATABASE SCOPED CREDENTIAL MyCredential
WITH IDENTITY = 'USER IDENTITY';
```

---

## External Data Source

Defines where external data is located.

Example:

```text
abfss://<storage-path>/Files/parquet/data1.parquet
```

---

## External File Format

Specifies the format of external files.

Supported formats include:

- CSV
- Parquet
- Delta

Example:

```sql
CREATE EXTERNAL FILE FORMAT MyFileFormat
WITH (
    FORMAT_TYPE = DELIMITEDTEXT,
    FORMAT_OPTIONS (
        FIELD_TERMINATOR = ',',
        STRING_DELIMITER = '"'
    )
);
```

---

## External Table

Creates a SQL table that references external data instead of storing it internally.

Example:

```sql
CREATE EXTERNAL TABLE MyExternalTable
(
    Column1 INT,
    Column2 NVARCHAR(50)
)
WITH
(
    LOCATION = 'myfolder/myfile.csv',
    DATA_SOURCE = MyExternalDataSource,
    FILE_FORMAT = MyFileFormat
);
```

---

# Mirroring vs. Data Virtualization

| Feature | Mirroring | Data Virtualization |
|----------|-----------|---------------------|
| Copies data | Yes | No |
| Storage Location | OneLake | External Source |
| Data Freshness | Near real-time replication | Live external access |
| ETL Required | No | No |
| Best For | Analytics on replicated operational data | Querying external data without duplication |

---

# Key Takeaways

- **Database Mirroring** continuously replicates Azure SQL Database data into **OneLake**.
- Mirroring provides **near real-time analytics** without traditional ETL.
- Replication status can be monitored through the **Replication** tab.
- **Data Virtualization** enables querying external data without moving or copying it.
- Supported external formats include **Parquet**, **CSV**, and **Delta**.
- Core virtualization components include:
  - Database Scoped Credentials
  - External Data Sources
  - External File Formats
  - External Tables
- Together, mirroring and data virtualization simplify enterprise data integration while reducing storage and maintenance costs.
