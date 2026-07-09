# 📘 Visualize Real-Time Data in Microsoft Fabric

## 🎯 Overview

After streaming data has been ingested and stored in an **Eventhouse (KQL Database)**, Microsoft Fabric provides tools to visualize the data in real time.

The two primary visualization options are:

1. **Real-Time Dashboards**
2. **Power BI Reports**

These tools help monitor live data, analyze trends, and support data-driven decision making.

---

# 📊 Real-Time Dashboards

## What is a Real-Time Dashboard?

A **Real-Time Dashboard** is an interactive dashboard that displays live streaming data from an **Eventhouse**.

It consists of multiple **tiles**, each representing a visualization generated from a **KQL query**.

Each tile automatically updates as new data arrives.

---

# 🏗 Dashboard Structure

A dashboard contains one or more **tiles**.

Each tile includes:

- A KQL query
- A visualization
- Interactive filtering capabilities

```text
Real-Time Dashboard
│
├── Tile 1 (KQL Query → Chart)
├── Tile 2 (KQL Query → Table)
├── Tile 3 (KQL Query → KPI)
└── Tile 4 (KQL Query → Graph)
```

---

# 📝 Creating a Real-Time Dashboard

There are two ways to create one:

## Option 1

Create a dashboard directly inside a **Fabric Workspace**.

---

## Option 2

Create a dashboard directly from a **KQL Queryset** in an **Eventhouse**.

---

# 📈 Dashboard Visualizations

Each dashboard tile is powered by a **KQL query**.

By default:

- Query results are displayed as a **table**.

You can customize the visualization into different chart types depending on your analysis needs.

---

# 🔍 Interactive Features

Published Real-Time Dashboards allow users to interact with the data.

Capabilities include:

- Drill into data
- Filter results
- Aggregate values
- Change visualization types
- Explore live metrics

These features help users investigate streaming events without modifying the underlying queries.

---

# 📊 Visualize with Power BI

In addition to Real-Time Dashboards, Microsoft Fabric allows you to build **Power BI reports** using data stored in a **KQL Database**.

Benefits include:

- Rich interactive reports
- Advanced visualizations
- Business dashboards
- Integration with other Power BI datasets
- Sharing across the organization

Power BI provides more comprehensive business intelligence capabilities, while Real-Time Dashboards focus on live operational monitoring.

---

# 📈 Visualization Workflow

```text
Streaming Data
       │
       ▼
 Eventstream
       │
       ▼
 Eventhouse
(KQL Database)
       │
       ├──────────────► Real-Time Dashboard
       │                  (Live Monitoring)
       │
       └──────────────► Power BI
                          (Business Reporting)
```

---

# 📝 Key Takeaways

- **Real-Time Dashboards** provide live monitoring of streaming data stored in an **Eventhouse**.
- Dashboards consist of multiple **tiles**, each powered by a **KQL query**.
- By default, query results appear as **tables**, but visualizations can be customized.
- Users can interact with dashboard tiles by drilling down, filtering, aggregating, and changing visualization types.
- Dashboards can be created:
  - From a **Fabric Workspace**
  - Directly from a **KQL Queryset**
- **Power BI** can also connect to **KQL Databases** to create interactive reports and business dashboards.

---

# 📌 Important Terms

| Term | Description |
|------|-------------|
| Real-Time Dashboard | Interactive dashboard for monitoring live streaming data |
| Tile | Individual visualization within a dashboard |
| KQL Query | Query used to retrieve data from an Eventhouse |
| KQL Queryset | Workspace for creating and managing KQL queries |
| Eventhouse | Storage location for streaming and time-series data |
| KQL Database | Database optimized for real-time analytics |
| Power BI | Business intelligence tool for creating interactive reports and dashboards |
