# 📘 Understand Data Warehouses

## 🎯 Overview

A **Data Warehouse** is a centralized repository designed for **analytics** and **reporting**. Unlike operational databases that support daily business transactions, data warehouses consolidate data from multiple sources into a structure optimized for querying and business intelligence.

---

# 🏗️ Data Warehouse Lifecycle

Building a modern data warehouse typically involves four stages:

## 1. Data Ingestion

Move data from various source systems into the data warehouse.

---

## 2. Data Storage

Store data in a structure optimized for analytical queries.

---

## 3. Data Processing

Transform and prepare data for reporting and analysis.

---

## 4. Data Analysis and Delivery

Generate business insights and deliver them through reporting tools and dashboards.

---

# 📊 Designing a Data Warehouse

Data warehouses organize data using **Dimensional Modeling**, a design approach optimized for analytical workloads.

Dimensional modeling groups measurable business events with descriptive business information, making data easier to query and analyze.

### Example

Analyze:

- Total sales
- Sales by store
- Sales by customer
- Sales by date

---

# 🗃️ Types of Tables

A dimensional model consists of two primary table types:

- **Fact Tables**
- **Dimension Tables**

---

# 📈 Fact Tables

## What are Fact Tables?

Fact Tables store measurable business events and numerical data.

They are the primary source for analytical calculations.

### Characteristics

- Large number of rows
- Numeric values
- Foreign keys to dimensions
- Records business events

### Examples

- Sales Amount
- Quantity Sold
- Profit
- Revenue
- Order Total

---

# 📋 Dimension Tables

## What are Dimension Tables?

Dimension Tables provide descriptive information that adds context to Fact Tables.

### Characteristics

- Fewer rows
- Descriptive attributes
- Used for filtering and grouping

### Examples

- Customer
- Product
- Store
- Employee
- Date

---

# 🔑 Keys in Dimension Tables

Dimension tables commonly contain two types of keys.

---

## Surrogate Key

A warehouse-generated unique identifier.

### Characteristics

- Integer value
- Created automatically
- Used internally by the warehouse
- Improves consistency and performance

Example:

```text
CustomerKey = 10025
```

---

## Alternate Key (Business Key)

A natural identifier from the source system.

### Characteristics

- Maintains traceability
- Represents real-world identifiers

Examples:

- Customer ID
- Product Code
- Employee Number

Example:

```text
CustomerID = CUST-1005
```

---

## Why Both Keys Are Needed

| Surrogate Key | Alternate Key |
|----------------|---------------|
| Internal warehouse identifier | Original source system identifier |
| Improves performance | Maintains business traceability |
| Stable even if source changes | Matches operational systems |

---

# 🕒 Special Types of Dimension Tables

Some dimensions provide additional analytical capabilities.

---

## Time Dimension

A Time Dimension enables analysis across time periods.

Typical columns include:

- Year
- Quarter
- Month
- Week
- Day

### Example Analyses

- Monthly sales
- Quarterly revenue
- Year-over-year growth

---

## Slowly Changing Dimensions (SCD)

Slowly Changing Dimensions (SCD) track changes to descriptive information over time.

### Examples

- Customer address changes
- Product price changes
- Employee department changes

### Benefits

- Historical reporting
- Trend analysis
- Accurate historical records

---

# ⭐ Schema Design

Transactional databases usually use **Normalization** to reduce duplication.

Data warehouses often use **Denormalization** to improve query performance.

---

# 🌟 Star Schema

## What is a Star Schema?

The most common dimensional model.

A single **Fact Table** connects directly to multiple **Dimension Tables**.

```text
           Product
              |
Customer — Fact Sales — Date
              |
           Store
              |
          Employee
```

---

## Advantages

- Simple design
- Fewer joins
- Fast analytical queries
- Easy to understand
- Ideal for Power BI

---

## Typical Fact Table

```text
FactSales

CustomerKey
ProductKey
DateKey
StoreKey
SalesAmount
Quantity
Profit
```

---

# ❄️ Snowflake Schema

## What is a Snowflake Schema?

A variation of the Star Schema where dimensions are **normalized** into additional related tables.

Example:

```text
FactSales
      |
 DimProduct
      |
 -------------------
 |                 |
DimCategory   DimSupplier
```

---

## Example

Instead of storing category and supplier information inside **DimProduct**, they are separated into:

- DimCategory
- DimSupplier

Similarly:

```text
DimCustomer
      |
DimGeography
```

and

```text
DimStore
      |
DimGeography
```

share the same geography information.

---

## Advantages

- Reduced data duplication
- Better maintenance
- Shared dimensions
- Improved consistency

---

## Disadvantages

- More joins
- Slightly more complex queries
- Can reduce query performance compared to Star Schema

---

# ⭐ Star Schema vs ❄️ Snowflake Schema

| Feature | Star Schema | Snowflake Schema |
|---------|-------------|------------------|
| Dimension Design | Denormalized | Normalized |
| Query Performance | Faster | Slightly slower |
| Number of Joins | Fewer | More |
| Ease of Understanding | Easier | More complex |
| Storage Efficiency | Lower | Higher |
| Common Usage | Most data warehouses | Large, complex warehouses |

---

# 📝 Key Takeaways

- A **Data Warehouse** centralizes data for analytics and reporting.
- Modern data warehouses follow four stages: **Ingestion, Storage, Processing, and Analysis**.
- **Dimensional Modeling** organizes data into Fact Tables and Dimension Tables.
- **Fact Tables** store measurable business events.
- **Dimension Tables** provide descriptive context for analysis.
- Dimension tables commonly contain both **Surrogate Keys** and **Alternate (Business) Keys**.
- **Time Dimensions** enable time-based analysis.
- **Slowly Changing Dimensions (SCDs)** preserve historical changes.
- **Star Schema** is the most common warehouse design because it simplifies queries and improves performance.
- **Snowflake Schema** normalizes dimensions to reduce redundancy while increasing complexity.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| Data Warehouse | Centralized repository optimized for analytics and reporting |
| Dimensional Modeling | Database design technique using Fact and Dimension tables |
| Fact Table | Stores measurable business events and numerical values |
| Dimension Table | Stores descriptive information for analysis |
| Surrogate Key | Warehouse-generated unique identifier |
| Alternate Key | Business or natural key from the source system |
| Time Dimension | Dimension used for date and time analysis |
| Slowly Changing Dimension (SCD) | Dimension that tracks historical attribute changes |
| Star Schema | Dimensional model with one Fact Table connected directly to Dimensions |
| Snowflake Schema | Normalized dimensional model with related Dimension Tables |
| Normalization | Reduces data duplication by separating related data |
| Denormalization | Combines related data to improve analytical query performance |
