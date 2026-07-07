# 📘 Ingest and Transform Real-Time Data in Microsoft Fabric

## 🎯 Overview

Microsoft Fabric **Real-Time Intelligence** provides two primary methods for ingesting streaming data:

1. **Eventstreams** – Ingest, transform, and route streaming data in real time.
2. **Direct Ingestion into a KQL Database (Eventhouse)** – Load data directly into a KQL database and transform it afterward using update policies.

---

# 🚀 Method 1: Eventstreams

## What is an Eventstream?

An **Eventstream** is a real-time data pipeline that:

- Ingests streaming data from multiple sources
- Optionally transforms the data
- Routes the processed data to one or more destinations

### Eventstream Workflow

```text
Data Sources
      │
      ▼
Transformations (Optional)
      │
      ▼
Destinations
```

Think of an Eventstream like a **water pipe system**:

- 🚰 **Source** → Faucet (where data originates)
- 🧹 **Transformation** → Water filter (cleans/processes data)
- 🪣 **Destination** → Bucket or sink (where processed data is stored)

---

# 📥 Eventstream Components

## 1. Data Sources

Eventstreams support a wide variety of streaming data sources.

### Microsoft Sources

- Azure Event Hubs
- Azure IoT Hub
- Azure Service Bus
- Change Data Capture (CDC)
- Other Microsoft services

### Azure Events

- Azure Blob Storage events

### Fabric Events

- Workspace item changes
- OneLake data changes
- Fabric job events

### External Sources

- Apache Kafka
- Google Cloud Pub/Sub
- MQTT *(Preview)*

> **Tip:** Eventstreams support many Microsoft and third-party streaming platforms.

---

# 🔄 Event Transformations

Raw streaming data often needs processing before analysis.

Eventstreams can transform data **while it is flowing**.

## Available Transformations

- SQL code
- Filter
- Manage fields
- Aggregate
- Group By
- Expand
- Join

### Benefits

- Clean incoming data
- Remove unnecessary fields
- Aggregate events
- Combine multiple streams
- Prepare data before storage

---

# 🎯 Event Destinations

Processed streaming data can be routed to several destinations.

Supported destinations include:

- **KQL Database (Eventhouse)**
- **Lakehouse**
- **Derived Stream**
- **Fabric Activator**
- **Custom Endpoint**

### Why Destinations Matter

Streaming data is temporary.

Destinations allow you to:

- Store data
- Query it
- Build dashboards
- Trigger alerts
- Automate workflows
- Integrate with other systems

---

# 🚀 Method 2: Direct Ingestion into Eventhouse

Instead of using an Eventstream, data can be loaded directly into a **KQL Database** inside an **Eventhouse**.

### Supported Sources

- Local files
- Azure Storage
- Amazon S3
- Azure Event Hubs
- OneLake
- Other supported connectors

Data ingestion is configured through:

- **Get Data**
- Built-in connectors

---

# 🔄 Data Transformation with Update Policies

When using **direct ingestion**, data transformation occurs **after** the data is stored.

This differs from Eventstreams.

---

## Eventstream vs Update Policy

### Eventstream

```text
Source
   │
Transform
   │
Store
```

Transformation happens **before** storage.

---

### KQL Database

```text
Source
   │
Store
   │
Update Policy
   │
Transformed Table
```

Transformation happens **after** storage.

---

# 🛠 Update Policies

An **Update Policy** automatically runs whenever new data arrives.

It:

1. Detects newly ingested data.
2. Executes a KQL query.
3. Transforms the data.
4. Stores the transformed results in another table.

### Benefits

- Automated processing
- No manual execution required
- Keeps destination tables continuously updated
- Supports complex transformation logic

---

# 📊 Comparison

| Feature | Eventstream | Direct KQL Ingestion |
|----------|-------------|----------------------|
| Primary Purpose | Stream processing | Data ingestion |
| Transformation Timing | Before storage | After storage |
| Processing Method | Built-in transformations | Update Policies |
| Routing Support | Yes | No |
| Multiple Destinations | Yes | No |
| Best For | Real-time pipelines | Direct ingestion into Eventhouse |

---

# 🔁 Overall Architecture

```text
Option 1

Streaming Source
        │
        ▼
   Eventstream
        │
   Transform Data
        │
        ▼
Destination
(KQL DB, Lakehouse, Activator, etc.)

-----------------------------------------

Option 2

Streaming Source
        │
        ▼
KQL Database (Eventhouse)
        │
        ▼
Update Policy
        │
        ▼
Transformed Table
```

---

# 🤖 AI Integration

Because Eventhouses are integrated with **OneLake**, transformed streaming data becomes available across Microsoft Fabric.

This enables:

- Power BI
- Copilot
- Fabric IQ
- Real-Time Dashboards
- Other Fabric workloads

to consume the same real-time data.

---

# 📝 Key Takeaways

- Microsoft Fabric supports **two methods** for ingesting streaming data:
  - **Eventstreams**
  - **Direct ingestion into a KQL Database (Eventhouse)**
- **Eventstreams** ingest, transform, and route streaming data in real time.
- Eventstreams consist of **Sources → Transformations → Destinations**.
- Supported sources include Microsoft services, Azure events, Fabric events, Apache Kafka, Google Pub/Sub, and MQTT.
- Built-in transformations include SQL, filtering, aggregation, grouping, joins, and field management.
- Eventstreams can send data to Eventhouses, Lakehouses, Activator, derived streams, or custom endpoints.
- Direct ingestion loads data directly into a **KQL Database**.
- **Update Policies** automatically transform newly ingested data after it is stored.
- Eventstream transformations occur **before storage**, while Update Policies occur **after storage**.
- Eventhouse data integrates with **OneLake**, making it available to Power BI, Copilot, Fabric IQ, and other Microsoft Fabric services.

---

# 📌 Important Terms

| Term | Description |
|------|-------------|
| Eventstream | Real-time pipeline for ingesting, transforming, and routing streaming data |
| Source | Origin of streaming data |
| Transformation | Processing applied to data before storage |
| Destination | Final location where processed data is stored or consumed |
| Eventhouse | Storage service for streaming and time-series data |
| KQL Database | Database optimized for real-time event analytics |
| Update Policy | Automatic transformation that runs after data is ingested into a KQL database |
| Derived Stream | New stream created from an existing Eventstream |
| CDC (Change Data Capture) | Streams database changes in real time |
| MQTT | Lightweight messaging protocol commonly used by IoT devices |
| Apache Kafka | Distributed event streaming platform |
| OneLake | Unified storage layer shared across Microsoft Fabric |
