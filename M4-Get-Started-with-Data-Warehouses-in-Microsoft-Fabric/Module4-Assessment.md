# Module Assessment – Analyze Data in a Microsoft Fabric Data Warehouse

**Score:** 200 XP  
**Estimated Time:** 10 Minutes

> **Note:**
> This assessment evaluates your understanding of the module. Unlike previous knowledge checks, you won't receive feedback for each individual question—only whether your final answers are correct or incorrect. Review the module content before attempting the assessment.

---

## Question 1

### In the context of a data warehouse star schema, what is the primary role of a dimension table?

- A. To store the numerical values that are analyzed for business insights.
- ✅ **B. To provide descriptive context for the numerical data stored in fact tables.**
- C. To act as a staging area for raw data before transformation.

### ✅ Correct Answer
**B. To provide descriptive context for the numerical data stored in fact tables.**

### Explanation

A **dimension table** stores descriptive attributes such as:

- Customer Name
- Product Category
- Date
- Location

These tables provide context for the numeric values stored in **fact tables**, making business analysis easier.

**Example**

| Fact Table | Dimension Table |
|------------|-----------------|
| Sales Amount | Product Name |
| Quantity Sold | Customer |
| Profit | Region |

---

## Question 2

### After implementing row-level security (RLS) in your Microsoft Fabric data warehouse, a user reports they cannot see any data in a specific table. What could be a potential cause?

- A. The user's role does not have column-level security permissions.
- B. The table does not have dynamic data masking enabled.
- ✅ **C. The user does not meet any condition in the RLS policy's predicate.**

### ✅ Correct Answer
**C. The user does not meet any condition in the RLS policy's predicate.**

### Explanation

**Row-Level Security (RLS)** filters rows based on user identity.

If the predicate evaluates to **FALSE** for every row, the user sees **no data**, even though they have permission to access the table.

---

## Question 3

### Which feature of a Fabric data warehouse allows you to perform cross-database querying without copying data?

- A. Using surrogate keys to link tables across databases.
- ✅ **B. Three-part naming convention to join tables from different databases.**
- C. Creating views that automatically synchronize data between databases.

### ✅ Correct Answer
**B. Three-part naming convention to join tables from different databases.**

### Explanation

Microsoft Fabric supports querying across databases using:

```sql
DatabaseName.SchemaName.TableName
```

This **three-part naming convention** allows joins without duplicating data.

Example:

```sql
SELECT *
FROM SalesDB.dbo.Sales s
JOIN CustomerDB.dbo.Customers c
ON s.CustomerID = c.CustomerID;
```

---

## Question 4

### When preparing a dimensional model in a Fabric data warehouse, you need to ensure unique identification of rows in the DimCustomer table. Which key should you implement?

- ✅ **A. Surrogate key to provide a unique identifier for each row.**
- B. Foreign key to ensure referential integrity with fact tables.
- C. Natural key to uniquely identify rows based on business logic.

### ✅ Correct Answer
**A. Surrogate key to provide a unique identifier for each row.**

### Explanation

A **surrogate key** is an artificial, system-generated key used as the primary key of a dimension table.

Example:

| CustomerKey | CustomerID | Name |
|-------------|------------|------|
| 1 | C001 | John |
| 2 | C002 | Mary |

Advantages:

- Never changes
- Faster joins
- Supports Slowly Changing Dimensions (SCD)

---

## Question 5

### Your organization needs to restrict access to sensitive customer data in your Microsoft Fabric data warehouse. Which feature should you implement to ensure only specific users can view certain rows of data?

- ✅ **A. Row-level security (RLS)**
- B. Dynamic data masking
- C. Column-level security (CLS)

### ✅ Correct Answer
**A. Row-level security (RLS)**

### Explanation

**RLS** restricts **rows** based on user identity.

Example:

| User | Visible Region |
|------|----------------|
| Alice | North |
| Bob | South |

Each user only sees the rows they are authorized to access.

---

## Question 6

### When using a snowflake schema in a data warehouse, how are dimension tables typically structured?

- A. All dimension attributes are stored in a single table to minimize join operations.
- B. Dimension tables contain only surrogate keys and no descriptive attributes.
- ✅ **C. Dimension tables are normalized and split into additional tables based on hierarchical relationships.**

### ✅ Correct Answer
**C. Dimension tables are normalized and split into additional tables based on hierarchical relationships.**

### Explanation

A **snowflake schema** normalizes dimension tables.

Example:

```
Product
   │
   ├── Category
   │
   └── Supplier
```

Advantages:

- Less redundancy
- Better data integrity

Disadvantages:

- More joins
- Slightly slower queries

---

## Question 7

### While querying a data warehouse, you notice that the query execution time is significantly longer than expected. Which T-SQL feature can you use to optimize performance?

- ✅ **A. Use indexes on frequently joined columns to speed up query execution.**
- B. Remove the WHERE clause to include more data.
- C. Increase the size of the result set returned by the query.

### ✅ Correct Answer
**A. Use indexes on frequently joined columns to speed up query execution.**

### Explanation

Indexes allow SQL Server or Fabric Warehouse to locate matching rows quickly.

Good candidates for indexing include:

- Foreign keys
- JOIN columns
- Frequently filtered columns
- ORDER BY columns

Indexes reduce full table scans and improve query performance.

---

## Question 8

### Which feature in Microsoft Fabric data warehouse allows you to restrict access to specific columns of data based on user identity?

- ✅ **A. Column-level security (CLS)**
- B. Dynamic data masking
- C. Row-level security (RLS)

### ✅ Correct Answer
**A. Column-level security (CLS)**

### Explanation

**Column-Level Security (CLS)** restricts access to specific columns.

Example:

| User | Can View Salary? |
|------|------------------|
| HR | ✅ Yes |
| Employee | ❌ No |

Unlike Dynamic Data Masking, CLS completely blocks unauthorized access.

---

## Question 9

### To perform an upsert operation on the DimProduct table in your Fabric data warehouse, which T-SQL statement should you use?

- ✅ **A. MERGE statement to perform the upsert operation by matching records.**
- B. DELETE statement followed by an INSERT statement.
- C. SELECT INTO statement to copy data.

### ✅ Correct Answer
**A. MERGE statement to perform the upsert operation by matching records.**

### Explanation

The **MERGE** statement combines:

- INSERT
- UPDATE
- DELETE (optional)

into a single operation.

Example:

```sql
MERGE DimProduct AS Target
USING NewProducts AS Source
ON Target.ProductID = Source.ProductID

WHEN MATCHED THEN
    UPDATE SET Target.Price = Source.Price

WHEN NOT MATCHED THEN
    INSERT (ProductID, ProductName, Price)
    VALUES (Source.ProductID, Source.ProductName, Source.Price);
```

This efficiently performs an **upsert** (update existing records and insert new ones).

---

# Answer Key

| Question | Answer |
|----------|--------|
| 1 | ✅ B |
| 2 | ✅ C |
| 3 | ✅ B |
| 4 | ✅ A |
| 5 | ✅ A |
| 6 | ✅ C |
| 7 | ✅ A |
| 8 | ✅ A |
| 9 | ✅ A |

---

# Key Concepts to Remember

- **Fact Table** → Stores measurable numeric data.
- **Dimension Table** → Stores descriptive attributes.
- **Star Schema** → Denormalized dimensions for faster queries.
- **Snowflake Schema** → Normalized dimensions with more joins.
- **Surrogate Key** → Artificial unique identifier.
- **Natural Key** → Business-generated identifier.
- **RLS** → Restricts rows.
- **CLS** → Restricts columns.
- **Dynamic Data Masking** → Masks sensitive values but does not prevent access.
- **MERGE** → Performs UPSERT operations.
- **Three-part naming** → Enables cross-database queries.
- **Indexes** → Improve JOIN and query performance.
