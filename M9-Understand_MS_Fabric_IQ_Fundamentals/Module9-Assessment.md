# Module Assessment – Introduction to Fabric IQ and Ontology Modeling

**Score:** 200 XP  
**Estimated Time:** 5 Minutes

This assessment evaluates your understanding of Microsoft Fabric IQ, ontology modeling, data agents, data binding, and Graph Query Language (GQL).

---

# Question 1

### What are the three core concepts that make up an ontology in Fabric IQ?

- A. Tables, columns, and foreign keys
- ✅ **B. Things (entity types), facts (properties), and connections (relationships)**
- C. Lakehouses, warehouses, and semantic models

## ✅ Correct Answer

**B. Things (entity types), facts (properties), and connections (relationships)**

### Explanation

An **ontology** in Microsoft Fabric IQ models the business domain rather than the physical data structure.

Its three core concepts are:

- **Things (Entity Types):** Business objects such as Customer, Product, or Employee.
- **Facts (Properties):** Attributes describing those entities, such as Name, Age, or Price.
- **Connections (Relationships):** How entities relate to one another, such as *Customer places Order*.

Unlike traditional databases, ontology focuses on business meaning instead of table design.

---

# Question 2

### What is the primary role of a Fabric data agent?

- A. To move data from lakehouses to warehouses
- B. To visualize relationships between entities in a graph
- ✅ **C. To process natural language questions and generate queries grounded in ontology definitions**

## ✅ Correct Answer

**C. To process natural language questions and generate queries grounded in ontology definitions**

### Explanation

A **Fabric data agent** acts as an AI-powered interface between users and data.

It:

- Accepts natural language questions
- Understands business concepts defined in the ontology
- Generates appropriate queries automatically
- Returns meaningful answers without requiring users to write SQL or KQL

Example:

> "What were the total sales in Region VI last quarter?"

The data agent interprets the request using the ontology and retrieves the correct data.

---

# Question 3

### How does data binding in ontology modeling differ from traditional ETL processes?

- A. Data binding copies data into a centralized warehouse, while ETL leaves data in place.
- ✅ **B. Data binding creates a semantic layer that references data in place, while ETL copies and transforms data into a warehouse.**
- C. Data binding and ETL are the same process with different names.

## ✅ Correct Answer

**B. Data binding creates a semantic layer that references data in place, while ETL copies and transforms data into a warehouse.**

### Explanation

**Data Binding** and **ETL** have different purposes:

| Data Binding | Traditional ETL |
|--------------|-----------------|
| References data where it already exists | Copies data into a warehouse |
| Creates a semantic layer | Transforms and loads data |
| No data duplication | Data is duplicated |
| Faster to implement | Requires ETL pipelines |

Fabric IQ uses **data binding** to connect ontology definitions directly to existing data sources without physically moving the data.

---

# Question 4

### Which Fabric IQ component uses GQL (Graph Query Language) for querying?

- A. Ontology items
- B. Data agents
- ✅ **C. Graph in Microsoft Fabric**

## ✅ Correct Answer

**C. Graph in Microsoft Fabric**

### Explanation

**Graph in Microsoft Fabric** uses **Graph Query Language (GQL)** to query and analyze relationships between entities.

It is designed for graph-based scenarios such as:

- Social networks
- Supply chains
- Fraud detection
- Knowledge graphs

GQL allows users to traverse and analyze connected data efficiently.

---

# Question 5

### What makes entity types different from traditional database tables?

- A. Entity types are tied to specific databases and schemas.
- ✅ **B. Entity types are reusable logical models that exist independently of any storage system.**
- C. Entity types can only contain static data, not time-series data.

## ✅ Correct Answer

**B. Entity types are reusable logical models that exist independently of any storage system.**

### Explanation

An **Entity Type** represents a business concept rather than a physical table.

For example:

- Customer
- Product
- Supplier
- Employee

These logical models:

- Are independent of databases or storage technologies
- Can map to multiple data sources
- Promote reuse across analytics and AI applications
- Focus on business semantics rather than implementation details

Unlike traditional tables, entity types are not constrained by a specific schema or database.

---

# 📚 Key Takeaways

| Concept | Remember |
|----------|----------|
| **Ontology** | Consists of **Things (Entity Types), Facts (Properties), and Connections (Relationships)** |
| **Entity Types** | Logical business objects independent of storage systems |
| **Properties** | Attributes describing an entity |
| **Relationships** | Connections between entity types |
| **Fabric Data Agent** | Uses AI to answer natural language questions based on the ontology |
| **Data Binding** | References data in place through a semantic layer without copying it |
| **Traditional ETL** | Copies, transforms, and loads data into a centralized repository |
| **Graph in Microsoft Fabric** | Uses **Graph Query Language (GQL)** for relationship-based queries |
| **Ontology Modeling** | Models business concepts instead of physical database structures |
