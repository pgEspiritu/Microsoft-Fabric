# Configure settings for scale

The semantic model is designed. The final step is configuring settings that allow it to scale as:

- Data volume grows
- More users access the model
- External tools connect
- AI workloads increase

These settings determine whether your semantic model can efficiently support enterprise workloads.

---

# Large semantic model storage format

The **Large Semantic Model Storage Format** changes how the semantic model stores and compresses data.

By default, Power BI limits uploaded models to **10 GB**.

When enabled:

- Models can exceed 10 GB.
- Maximum size depends on the Fabric capacity.
- Supports enterprise-scale datasets.

> **Note:** Direct Lake semantic models automatically enable this setting. Import models require manual configuration.

---

## Why enable it?

Enable Large Semantic Model Storage Format when:

- Your model exceeds **10 GB**.
- You need **XMLA endpoint read/write** access.
- You plan to use **Query Scaleout**.
- You use **Incremental Refresh** with partitions.

---

# XMLA endpoint read/write access

The **XMLA Endpoint** allows external tools to connect directly to the semantic model.

Common tools include:

- Tabular Editor
- DAX Studio
- ALM Toolkit
- Analysis Services client libraries

These tools support advanced model development that isn't available through the Fabric web interface.

---

## Prerequisite

Before enabling XMLA Read/Write:

- Large Semantic Model Storage Format **must already be enabled**.

---

## What XMLA enables

### Tabular Editor

- Advanced model editing
- Calculation Groups
- Best Practice Analyzer
- Source control integration

---

### DAX Studio

- Analyze DAX queries
- Measure performance
- Query plans
- Server timings

---

### ALM Toolkit

- Compare semantic models
- Deploy model changes
- Synchronize environments

---

### CI/CD

Deploy semantic models automatically using:

- Azure DevOps
- GitHub Actions
- Analysis Services libraries

This is essential for enterprise development.

---

# Query Scaleout

Normally:

```
Users
   ↓
One Semantic Model
```

Hundreds of simultaneous users can overload a single model instance.

---

## Query Scaleout solution

Query Scaleout creates multiple **read-only replicas**.

```
            Replica 1
           /
Users ─── Primary Model
           \
            Replica 2
             \
              Replica 3
```

Incoming queries are distributed across replicas.

Benefits:

- Higher concurrency
- Faster report loading
- Better performance during peak hours

---

## Synchronization

Replicas synchronize after each model refresh.

Because synchronization isn't instantaneous:

- Primary model refreshes first.
- Replicas update shortly afterward.
- A brief delay may occur before replicas show new data.

---

## Prerequisite

Query Scaleout requires:

- Large Semantic Model Storage Format

---

## When to enable Query Scaleout

Enable when:

- Hundreds of users access the same model.
- Query performance slows during peak periods.
- Fabric capacity supports replicas.

---

# Direct Lake fallback configuration

Direct Lake normally reads:

```
Delta Tables
      ↓
OneLake
      ↓
Memory
```

Some queries cannot execute directly in Direct Lake.

Fabric then switches to **DirectQuery**.

This behavior is called **Fallback**.

---

## Option 1 — Allow fallback (Default)

```
Direct Lake
      ↓
Unsupported Query
      ↓
DirectQuery
```

Advantages:

- Users always receive results.
- Higher compatibility.

Disadvantages:

- Slower performance.

---

## Option 2 — Disallow fallback

```
Direct Lake
      ↓
Unsupported Query
      ↓
Error
```

Advantages:

- Predictable performance.
- No unexpected DirectQuery execution.

Disadvantages:

- Unsupported queries fail.

---

## Best practice

For production:

Start with:

```
Allow fallback
```

Monitor:

- Which queries trigger fallback.
- Optimize DAX.
- Improve data model.

After optimization:

If every query stays within Direct Lake capabilities, consider:

```
Disallow fallback
```

---

# OneLake integration

OneLake Integration allows other Fabric workloads to consume semantic model data.

Instead of rebuilding business logic:

```
Semantic Model
      ↓
OneLake
      ↓
Notebook
Pipeline
Lakehouse
Data Science
Other Fabric Items
```

The semantic model becomes a reusable enterprise data source.

---

## Benefits

Other Fabric workloads can reuse:

- Clean star schema
- Business-friendly columns
- Curated datasets

without recreating transformations.

---

## When to enable

Enable OneLake Integration when:

- Data Scientists use notebooks.
- Data Engineers build pipelines.
- Multiple Fabric workloads need curated business data.
- Teams want a shared enterprise data source.

---

## Current limitation

OneLake Integration currently exports only:

- Import tables

It does **not** export:

- Direct Lake tables
- DirectQuery tables
- Measures
- Calculation Groups

> **Note:** Direct Lake data already exists in OneLake as Delta tables, making separate export unnecessary.

---

# Settings decision framework

| Setting | Default | Enable When |
|----------|----------|-------------|
| Large Semantic Model Storage Format | Off (automatic for Direct Lake) | Models exceed 10 GB, XMLA access, Query Scaleout, Incremental Refresh |
| XMLA Endpoint Read/Write | Read-only | External tools need to modify or deploy the model |
| Query Scaleout | Off | High user concurrency affects performance |
| Direct Lake Fallback | Allowed | Keep enabled initially; disable only after optimizing all queries |
| OneLake Integration | Off | Other Fabric workloads need curated semantic model data |

---

# Recommended configuration

### Small models

- Standard Storage
- No Query Scaleout
- XMLA Read-only
- Allow Direct Lake Fallback

---

### Medium enterprise models

- Large Semantic Model
- XMLA Read/Write
- Allow Fallback
- OneLake Integration

---

### Large enterprise deployment

- Large Semantic Model
- XMLA Read/Write
- Query Scaleout
- OneLake Integration
- Optimized Direct Lake queries
- Consider disabling fallback after validation

---

# Key Takeaways

- **Large Semantic Model Storage Format** removes the 10 GB limitation and enables enterprise features.
- **XMLA Endpoint Read/Write** allows advanced model development using external tools like Tabular Editor and DAX Studio.
- **Query Scaleout** improves performance by distributing queries across read-only replicas.
- **Direct Lake Fallback** automatically switches unsupported queries to DirectQuery; monitor and optimize before disabling it.
- **OneLake Integration** enables other Fabric workloads to consume curated semantic model data without rebuilding transformations.
- Together, these settings prepare semantic models for enterprise-scale reporting, collaboration, and AI-powered analytics.
