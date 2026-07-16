# Choose a Storage Mode (Semantic Models in Microsoft Fabric)

The **storage mode** determines **how data is accessed and stored** in a semantic model. It directly impacts:

- Query performance
- Data freshness
- Model size
- Available Fabric features
- AI capabilities (Copilot, Fabric IQ)

For Microsoft Fabric, **Direct Lake is the recommended default**.

---

# Storage Modes

## 1. Direct Lake (Recommended)

### Overview

Direct Lake is the default storage mode for semantic models in Microsoft Fabric.

Unlike Import mode, it **does not copy data** into the semantic model.

Unlike DirectQuery, it **does not generate SQL queries** against the source.

Instead, it reads **Delta Parquet files directly from OneLake**.

```text
Power BI

↓

Semantic Model

↓

OneLake Delta Tables

↓

Load columns into memory on demand
```

### Advantages

- Near real-time data
- No scheduled refresh
- Fast query performance
- Reads directly from Delta files
- Supports large semantic models automatically
- Best for Fabric-native workloads

### Automatic Features

Direct Lake automatically enables:

- Large Semantic Model Storage Format
- Query Scale-Out
- XMLA Read/Write Endpoint

No manual configuration required.

---

# Direct Lake Connection Options

## Option 1: OneLake Tables

```text
Power BI

↓

Semantic Model

↓

Lakehouse / Warehouse Delta Tables
```

Use when:

- Data exists in one Lakehouse
- Simple architecture
- Highest performance

---

## Option 2: SQL Analytics Endpoint

```text
Power BI

↓

Semantic Model

↓

SQL Analytics Endpoint

↓

Lakehouse / Warehouse
```

Use when you need:

- SQL Views
- Cross-database queries
- Row-Level Security (RLS)
- SQL-based business logic

---

# Direct Lake Fallback

Sometimes Direct Lake cannot execute a query efficiently.

Examples:

- Very complex DAX
- Memory limitations
- Unsupported operations

When this happens:

```text
Direct Lake

↓

Fallback

↓

DirectQuery

↓

SQL Analytics Endpoint
```

---

## Fallback Settings

### Allow Fallback

Pros

- User always gets results
- Automatic recovery

Cons

- Query may become slower

Recommended for production.

---

### Disallow Fallback

Pros

- Consistent performance

Cons

- Unsupported queries return errors

Useful for strict performance requirements.

---

# 2. Import Mode

## Overview

Import mode copies data into the semantic model.

```text
Source

↓

Copy Data

↓

Power BI Memory

↓

Reports
```

---

## Advantages

- Fastest query performance
- Highly compressed
- No dependency on source during queries

---

## Disadvantages

- Requires scheduled refresh
- Data becomes outdated between refreshes
- Larger model size

---

## Best Use Cases

- External data sources
- On-premises SQL Server
- CSV files
- APIs
- Maximum query performance
- Data changes infrequently

---

## Optimization Tips

- Connect to Views instead of raw tables
- Remove unnecessary columns
- Use efficient data types
- Reduce model size

---

# 3. DirectQuery Mode

## Overview

DirectQuery never stores data inside Power BI.

Every report interaction sends a query to the source.

```text
Power BI

↓

SQL Query

↓

Source Database

↓

Results
```

---

## Advantages

- Near real-time data
- No scheduled refresh
- Small model size
- Source remains the single source of truth

---

## Disadvantages

- Slowest performance
- Depends on source database performance
- High query latency

---

## Best Use Cases

- Very large databases
- Live operational systems
- External databases
- Strict governance requirements

---

# 4. Composite Mode

## Overview

Composite mode combines multiple storage modes in one semantic model.

Example:

```text
Fact Sales

↓

Direct Lake

+

Customer Table

↓

Import

+

CRM Data

↓

DirectQuery
```

---

## Advantages

- Maximum flexibility
- Supports multiple data sources
- Supports hybrid architectures
- Supports many-to-many relationships

---

## Best Use Cases

- Fabric + external databases
- Hybrid analytics
- Mixed refresh requirements

---

# Storage Mode Comparison

| Storage Mode | Data Location | Query Speed | Data Freshness | Scheduled Refresh | Best For |
|--------------|--------------|-------------|----------------|-------------------|----------|
| Direct Lake | OneLake Delta Tables | Fast | Near Real-Time | No | Fabric-native analytics |
| Import | In-memory semantic model | Fastest | Depends on refresh | Yes | Maximum performance |
| DirectQuery | Source database | Depends on source | Near Real-Time | No | Live operational systems |
| Composite | Mixed | Mixed | Mixed | Mixed | Hybrid solutions |

---

# Decision Flow

```text
Is your data stored in OneLake?

│

├── Yes
│      │
│      ├── Need SQL Views or RLS?
│      │
│      ├── Yes → Direct Lake via SQL Analytics Endpoint
│      │
│      └── No → Direct Lake via OneLake Tables
│
└── No
       │
       ├── Need live data?
       │
       ├── Yes → DirectQuery
       │
       └── No → Import
```

---

# Storage Mode Architecture

```text
                Data Sources
                     │
      ┌──────────────┼───────────────┐
      │              │               │
      ▼              ▼               ▼
 OneLake        SQL Database      External DB
      │              │               │
      ├──────────────┼───────────────┤
                     ▼
             Semantic Model
                     │
      ┌──────────────┼───────────────┐
      │              │               │
      ▼              ▼               ▼
 Direct Lake      Import        DirectQuery
                     │
                     ▼
               Power BI Reports
                     │
                     ▼
         Copilot / Fabric IQ / AI
```

---

# Best Practices

## Direct Lake

✅ Default choice for Fabric

- Use for Lakehouse and Warehouse data
- Keep Delta tables optimized
- Monitor fallback behavior

---

## Import

Use when:

- Data is external
- Refresh schedule is acceptable
- Maximum performance is required

---

## DirectQuery

Use when:

- Live data is required
- Source data is extremely large
- Data cannot be copied

---

## Composite

Use when:

- Combining Fabric and non-Fabric data
- Different tables require different storage modes
- Hybrid analytics solutions

---

# Key Takeaways

- **Direct Lake** is the recommended default for Microsoft Fabric.
- **Import** provides the fastest performance but requires scheduled refreshes.
- **DirectQuery** provides live access to external data but depends on source performance.
- **Composite** combines multiple storage modes for hybrid scenarios.
- Direct Lake automatically enables **Large Semantic Models**, **Query Scale-Out**, and **XMLA Read/Write**.
- Storage mode affects both **report performance** and **AI-powered experiences** such as Copilot and Fabric IQ.
