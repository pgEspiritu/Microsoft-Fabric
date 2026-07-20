# Module Assessment – Design Scalable Semantic Models in Microsoft Fabric

**Score:** 200 XP  
**Estimated Time:** 3 Minutes

This assessment evaluates your understanding of semantic model optimization in Microsoft Fabric, including Direct Lake, calculation groups, XMLA endpoints, referential integrity, and aggregation tables.

---

# Question 1

### An analytics team builds a new semantic model in Microsoft Fabric with all data stored in a lakehouse. Which storage mode should they choose as the default for this model?

- A. Import mode, because it provides the fastest query performance.
- ✅ **B. Direct Lake mode, because it reads Delta tables directly from OneLake without importing data.**
- C. DirectQuery mode, because it queries the source in real time.

## ✅ Correct Answer

**B. Direct Lake mode, because it reads Delta tables directly from OneLake without importing data.**

### Explanation

**Direct Lake** is the recommended storage mode when data resides in a **Microsoft Fabric Lakehouse**.

Benefits include:

- Reads **Delta tables directly from OneLake**
- No data import or scheduled refresh required
- Near Import-mode performance
- Lower latency than DirectQuery

Comparison:

| Storage Mode | Best Use Case |
|--------------|---------------|
| **Direct Lake** | Fabric Lakehouse (OneLake) ✅ |
| Import | Smaller datasets requiring in-memory storage |
| DirectQuery | External data sources requiring live queries |

---

# Question 2

### A company has 60 base measures in a semantic model and needs Year-to-Date (YTD), Quarter-to-Date (QTD), and Month-to-Date (MTD) versions of each. What should a model designer implement to avoid creating 180 additional measures?

- ✅ **A. A calculation group with time intelligence calculation items that use `SELECTEDMEASURE()`.**
- B. DAX variables to store intermediate results.
- C. Aggregations with pre-summarized tables.

## ✅ Correct Answer

**A. A calculation group with time intelligence calculation items that use `SELECTEDMEASURE()`.**

### Explanation

**Calculation Groups** eliminate the need to create multiple versions of the same measure.

Instead of creating:

- Sales
- Sales YTD
- Sales QTD
- Sales MTD
- Profit
- Profit YTD
- ...

You create:

- One base measure
- One calculation group containing:
  - YTD
  - QTD
  - MTD

Using:

```DAX
SELECTEDMEASURE()
```

The calculation group dynamically applies the selected time intelligence calculation to any measure.

This greatly reduces maintenance and keeps the semantic model scalable.

---

# Question 3

### A model designer needs to use Tabular Editor for external model development and deploy through CI/CD pipelines. Which setting is a prerequisite for XMLA endpoint read/write access?

- ✅ **A. Large semantic model storage format.**
- B. OneLake integration.
- C. Query scaleout.

## ✅ Correct Answer

**A. Large semantic model storage format.**

### Explanation

To enable **XMLA read/write** access (required for tools like **Tabular Editor**, **ALM Toolkit**, and CI/CD deployments), the semantic model must use the **Large semantic model storage format**.

This setting enables:

- External model editing
- Metadata deployment
- DevOps and CI/CD workflows
- Advanced model management

---

# Question 4

### A model designer enables the **Assume referential integrity** setting on a relationship between a fact table and a dimension table in a Direct Lake model. What is the performance benefit?

- ✅ **A. The engine uses INNER joins instead of LEFT OUTER joins, which reduces the number of rows processed.**
- B. The engine caches relationship metadata.
- C. The engine creates an index on the foreign key column.

## ✅ Correct Answer

**A. The engine uses INNER joins instead of LEFT OUTER joins, which reduces the number of rows processed.**

### Explanation

When **Assume Referential Integrity** is enabled, the engine assumes that every foreign key in the fact table has a matching primary key in the dimension table.

As a result, it can use:

- **INNER JOIN**

instead of:

- **LEFT OUTER JOIN**

Benefits:

- Fewer rows processed
- Faster query execution
- Improved performance for Direct Lake and DirectQuery models

---

# Question 5

### A semantic model has a fact table with **150 million rows**. Report users primarily view monthly and quarterly summaries by region. Which design pattern improves query performance for these summary-level visuals?

- ✅ **A. Aggregation tables that store precalculated totals at the monthly and quarterly grain.**
- B. Calculation groups with time intelligence calculation items.
- C. Bi-directional filtering between the fact and dimension tables.

## ✅ Correct Answer

**A. Aggregation tables that store precalculated totals at the monthly and quarterly grain.**

### Explanation

**Aggregation tables** store summarized data, allowing Power BI to answer common queries without scanning the detailed fact table.

Instead of reading all **150 million rows**, Power BI can query a much smaller table containing:

| Month | Region | Total Sales |
|--------|--------|-------------|
| Jan | North | 5,200,000 |
| Feb | North | 4,900,000 |

Benefits:

- Faster report rendering
- Reduced resource usage
- Better scalability for large semantic models

Calculation groups affect calculations, not storage, while bi-directional filtering often reduces performance and should only be used when necessary.

---

# 📚 Key Takeaways

| Concept | Remember |
|----------|----------|
| **Direct Lake** | Default storage mode for Fabric Lakehouse data; reads Delta tables directly from OneLake |
| **Calculation Groups** | Reuse calculations (e.g., YTD, QTD, MTD) with `SELECTEDMEASURE()` instead of creating duplicate measures |
| **Large Semantic Model Storage Format** | Required for XMLA read/write access, Tabular Editor, and CI/CD deployment |
| **Assume Referential Integrity** | Enables **INNER JOIN** instead of **LEFT OUTER JOIN** for improved query performance |
| **Aggregation Tables** | Store precomputed summaries to speed up queries on very large fact tables |
| **Query Scaleout** | Improves concurrent query performance but is **not** required for XMLA access |
| **OneLake Integration** | Provides unified storage but is unrelated to XMLA endpoint configuration |
