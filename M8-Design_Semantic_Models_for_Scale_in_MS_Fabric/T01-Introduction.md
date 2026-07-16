# Microsoft Fabric Learning Summary

## 1. Lakehouse

### What is a Lakehouse?

A **Lakehouse** combines the flexibility of a **Data Lake** with the analytical power of a **Data Warehouse**.

```text
Data Lake
- Stores any type of data
- Cheap storage
- Flexible

        +

Data Warehouse
- SQL querying
- ACID transactions
- Optimized analytics

        =

Lakehouse
```

### Storage Structure

```text
Lakehouse
│
├── Files
│     • CSV
│     • JSON
│     • Images
│     • Parquet
│     • Documents
│
└── Tables
      • Delta Tables
      • SQL Queryable
      • Power BI Ready
```

### Delta Lake

Provides:

- ACID Transactions
- Schema Enforcement
- Time Travel
- UPDATE / DELETE support
- Transaction Log
- Parquet Storage

### Data Ingestion Methods

- Upload files
- Load to Table
- Dataflows Gen2
- Spark Notebooks
- Data Factory Pipelines

### Transform Data

Using:

- Spark Notebooks
- PySpark
- Spark SQL
- Dataflows Gen2
- Pipelines

### Query Lakehouse

#### SQL Analytics Endpoint

Read-only SQL.

Supports:

- SELECT
- JOIN
- Views
- Row-Level Security (RLS)
- Column-Level Security (CLS)

Cannot:

- INSERT
- UPDATE
- DELETE

#### Spark Notebook

Languages:

- SQL
- PySpark
- Scala

Good for:

- Machine Learning
- Data Engineering
- Complex Transformations

#### Power BI

Supports:

- Direct Lake
- Semantic Models
- Copilot

---

# 2. Data Warehouse

## Purpose

A structured analytical database optimized for Business Intelligence (BI).

## Star Schema

```text
          Dim Date
              |
Dim Product - Fact Sales - Dim Customer
              |
         Dim Store
```

### Fact Table

Contains measurable business events:

- Sales
- Revenue
- Quantity
- Profit

### Dimension Table

Contains descriptive information:

- Customer
- Product
- Store
- Date

### Dimension Keys

#### Surrogate Key

Internal warehouse key.

```text
CustomerKey
1
2
3
```

#### Alternate Key

Business key from source systems.

```text
CustomerID
C100
C200
C300
```

### Slowly Changing Dimension (SCD)

Tracks historical changes.

Example:

```text
Customer

2024
Address = Manila

2025
Address = Cebu
```

History is preserved instead of overwritten.

### Warehouse Features

Supports full T-SQL.

#### DDL

- CREATE
- ALTER
- DROP

#### DML

- INSERT
- UPDATE
- DELETE
- MERGE

### Warehouse Ingestion

- COPY INTO
- OPENROWSET
- Pipelines
- Dataflows
- Cross-Database Queries

### Staging Pattern

```text
CSV

↓

Staging Table

↓

Transformation

↓

Dimension Tables

↓

Fact Tables
```

### Table Clone

Zero-copy clone.

```text
Original Table

↓

Clone

Same data

Different metadata
```

### Security

Workspace Roles:

- Admin
- Member
- Contributor
- Viewer

SQL Security:

- Object-Level Security
- Row-Level Security (RLS)
- Column-Level Security (CLS)
- Dynamic Data Masking

### Monitoring

Query Insights

- Long-running queries
- Query history
- Performance analysis

Dynamic Management Views (DMVs)

Example:

```sql
SELECT *
FROM sys.dm_exec_requests;
```

---

# 3. Real-Time Intelligence

## Purpose

Analyze streaming data with minimal latency.

### Event

A single occurrence.

Example:

```text
Temperature = 82°C
```

### Stream

A sequence of events over time.

```text
82

83

84

85

86
```

## Components

```text
Source

↓

Eventstream

↓

Transformation

↓

Destination
```

### Eventstream

#### Sources

- Azure Event Hub
- Azure IoT Hub
- Azure Service Bus
- CDC
- Kafka
- MQTT
- Fabric Events

#### Transformations

- SQL
- Filter
- Aggregate
- Join
- Group By
- Expand

#### Destinations

- Eventhouse
- Lakehouse
- Activator
- Derived Stream
- Custom Endpoint

### Eventhouse

Stores streaming data.

Uses:

- KQL Database

Optimized for:

- Time-series
- Fast ingestion

### KQL Queryset

Supports:

- KQL
- T-SQL

### Real-Time Dashboard

- Auto-refresh
- Interactive dashboards
- Live monitoring

### Activator

Automates actions.

```text
Events

↓

Objects

↓

Properties

↓

Rules

↓

Action
```

Examples:

- Email alerts
- Run Notebook
- Trigger Pipeline
- Power Automate workflow

---

# 4. Data Science

## Purpose

Train Machine Learning models.

### Machine Learning Types

#### Classification

Predicts categories.

Example:

```text
Will customer churn?
```

#### Regression

Predicts numbers.

```text
House Price
```

#### Clustering

Groups similar records.

#### Forecasting

Predicts future values.

```text
Sales Next Month
```

## Data Science Workflow

```text
Problem

↓

Collect Data

↓

Prepare Data

↓

Train Model

↓

Evaluate

↓

Predict

↓

Deploy
```

## Fabric Data Science Stack

```text
Lakehouse

↓

Notebook

↓

Spark

↓

Python

↓

MLflow

↓

Model Registry

↓

Predict
```

### Notebook Languages

- PySpark
- Spark SQL
- SparkR

### Data Wrangler

Low-code data preparation.

Features:

- Data profiling
- Missing value detection
- Automatic code generation

### MLflow

Tracks:

- Parameters
- Metrics
- Artifacts

```text
Experiment

├── Run 1

├── Run 2

└── Run 3
```

### Registered Models

Version control for ML models.

```text
SalesModel

Version 1

Version 2

Version 3
```

### PREDICT Function

Uses registered ML models for batch predictions.

---

# 5. SQL Database in Microsoft Fabric

## Overview

Based on Azure SQL Database.

Difference:

| Azure SQL Database | SQL Database in Fabric |
|--------------------|------------------------|
| PaaS | SaaS |

### Major Feature

```text
SQL Database

↓

Automatic Replication

↓

OneLake

↓

Parquet

↓

Analytics Ready
```

### Create Database

Options:

- Sample Data
- T-SQL Editor
- Connection Strings

### Source Control

Supports:

- Commit
- Pull
- History
- Collaboration

### Performance Dashboard

Shows:

- Query performance
- Bottlenecks
- Automatic indexes

### Automatic Tuning

Uses machine learning to:

- Create indexes
- Drop unused indexes
- Improve performance

### Security

- Workspace Roles
- Item Permissions
- Database Roles
- Row-Level Security
- Column-Level Security
- Dynamic Data Masking

### Copilot

Can:

- Generate SQL
- Explain SQL
- Fix SQL
- Auto-complete SQL

### Mirroring

```text
Azure SQL

↓

Fabric SQL

↓

OneLake

↓

Power BI

↓

Spark
```

Near real-time synchronization.

### Data Virtualization

Query external data without copying.

Supports:

- Parquet
- CSV
- Delta
- OneLake
- External Tables

---

# 6. Semantic Models

## Purpose

Business layer between raw data and reports.

## Storage Modes

### Import

```text
Power BI

↓

Copies Data

↓

Fast

↓

Manual Refresh Required
```

### DirectQuery

```text
Power BI

↓

Source Database

↓

Always Current

↓

Slower Queries
```

### Direct Lake

```text
Power BI

↓

OneLake Parquet

↓

No Copy

↓

Very Fast

↓

Always Current
```

Recommended storage mode for Microsoft Fabric.

## Star Schema

```text
Dimensions

↓

Fact

↓

Measures
```

## Relationships

Many-to-One

```text
Fact Sales

↓

Customer
```

Cross-filter direction:

- Single Direction (recommended)

## Views

Reusable SQL logic.

## Measures

Reusable DAX calculations.

Example:

```DAX
Total Sales =
SUM(Sales[Amount])
```

## Semantic Model Benefits

- Single source of truth
- Faster Power BI reports
- Copilot ready
- Fabric IQ ready
- Reusable business logic

---

# End-to-End Microsoft Fabric Architecture

```text
                 DATA SOURCES
      (ERP, CSV, IoT, SQL, APIs, Files)
                      │
                      ▼
          ┌──────────────────────┐
          │ Data Factory /       │
          │ Eventstreams /       │
          │ Dataflows            │
          └──────────────────────┘
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
     Lakehouse               Data Warehouse
 (Files + Delta Tables)    (Structured SQL)
          │                       │
          └───────────┬───────────┘
                      ▼
              OneLake Storage
                      │
          ┌───────────┼────────────┐
          ▼           ▼            ▼
     Spark       SQL Endpoint   Eventhouse
   Notebooks                    (KQL)
          │           │            │
          └───────────┼────────────┘
                      ▼
              Semantic Model
                      │
          ┌───────────┼────────────┐
          ▼           ▼            ▼
       Power BI    Copilot     Fabric IQ
                      │
                      ▼
               Business Insights
```

## Microsoft Fabric Workloads Summary

| Workload | Primary Purpose | Main Technologies |
|-----------|-----------------|-------------------|
| Lakehouse | Unified storage for structured and unstructured data | Delta Lake, Spark, SQL |
| Data Warehouse | Relational analytics | T-SQL, Star Schema |
| Real-Time Intelligence | Streaming analytics | Eventstream, Eventhouse, KQL, Activator |
| Data Science | Machine Learning | Spark, MLflow, Python |
| SQL Database | Operational database | Azure SQL Engine, OneLake |
| Semantic Models | BI semantic layer | DAX, Direct Lake, Power BI |
