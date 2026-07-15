# Module Assessment – SQL Database in Microsoft Fabric

**Score:** 200 XP  
**Estimated Time:** 8 Minutes

This assessment evaluates your understanding of SQL Database in Microsoft Fabric, including OneLake integration, performance monitoring, security, and AI-assisted querying.

---

# Question 1

### What is one of the capabilities of SQL Database in Microsoft Fabric that differentiates it from Azure SQL Database?

- A. It requires complex ETL processes for data analytics.
- ✅ **B. It automatically replicates data into OneLake and converts it to Parquet in near real-time.**
- C. It doesn't support integration with other services within Fabric.

## ✅ Correct Answer

**B. It automatically replicates data into OneLake and converts it to Parquet in near real-time.**

### Explanation

One of the key advantages of **SQL Database in Microsoft Fabric** is **automatic mirroring to OneLake**.

This capability:

- Replicates transactional data into **OneLake**
- Converts the data to the **Parquet** format
- Makes the data available for analytics in **near real-time**
- Eliminates the need for complex ETL pipelines

This seamless integration enables analytics tools like Power BI, Spark, and Data Engineering workloads to access the same data efficiently.

---

# Question 2

### How can you monitor the performance of a SQL database in Microsoft Fabric?

- ✅ **A. By using the performance dashboard in the Fabric portal.**
- B. By manually checking each query's performance.
- C. By using an external third-party tool exclusively.

## ✅ Correct Answer

**A. By using the performance dashboard in the Fabric portal.**

### Explanation

Microsoft Fabric provides a built-in **Performance Dashboard** that allows administrators and developers to monitor:

- Query execution performance
- Resource utilization
- Database activity
- Performance bottlenecks

Using the integrated dashboard is more efficient than manually reviewing queries or relying solely on external tools.

---

# Question 3

### What feature allows administrators to shield sensitive data from unauthorized access in SQL Database in Microsoft Fabric?

- ✅ **A. Object-level security**
- B. Graphical user interface management.
- C. Complex mathematical calculations.

## ✅ Correct Answer

**A. Object-level security**

### Explanation

**Object-level security** controls access to database objects such as:

- Tables
- Views
- Stored procedures
- Schemas

By assigning permissions, administrators can ensure that only authorized users can access sensitive database objects.

This helps protect confidential information and supports secure database management.

---

# Question 4

### What is the benefit of the natural language to SQL capability in SQL Database in Fabric?

- ✅ **A. It translates natural language queries into SQL within the query editor.**
- B. It manages graphical user interfaces.
- C. It performs complex data manipulation.

## ✅ Correct Answer

**A. It translates natural language queries into SQL within the query editor.**

### Explanation

SQL Database in Microsoft Fabric includes **AI-powered Natural Language to SQL** capabilities.

Users can type requests such as:

> "Show total sales by region for the last 30 days."

The query editor automatically generates the equivalent SQL statement, making it easier for users who are less familiar with SQL syntax to analyze data.

This feature:
- Improves productivity
- Reduces SQL coding effort
- Makes data querying more accessible

---

# 📚 Key Takeaways

| Concept | Remember |
|----------|----------|
| **OneLake Integration** | Automatically mirrors SQL data to OneLake in Parquet format for near real-time analytics |
| **Performance Dashboard** | Built-in tool for monitoring database performance and resource usage |
| **Object-level Security** | Controls access to tables, views, stored procedures, and other database objects |
| **Natural Language to SQL** | Uses AI to convert plain-language requests into SQL queries |
| **Parquet Format** | Optimized columnar storage format for analytics workloads |
| **Near Real-Time Mirroring** | Eliminates the need for complex ETL pipelines for analytics |
