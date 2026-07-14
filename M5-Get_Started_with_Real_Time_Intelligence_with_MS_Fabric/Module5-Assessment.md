# Module Assessment – Microsoft Fabric Real-Time Intelligence

**Score:** 200 XP  
**Estimated Time:** 10 Minutes

This assessment evaluates your understanding of Microsoft Fabric Real-Time Intelligence, including Eventstreams, Eventhouse, Activator, Real-Time Dashboards, and Kusto Query Language (KQL).

---

# Question 1

### Your company wants to optimize delivery routes in real-time to avoid delays caused by traffic congestion. Which component of Microsoft Fabric Real-Time Intelligence should be used to automatically trigger rerouting when a traffic pattern is detected?

- A. Real-Time Dashboards
- B. Eventstreams
- ✅ **C. Activator**

## ✅ Correct Answer

**C. Activator**

### Explanation

**Activator** continuously monitors incoming events and automatically performs actions when predefined conditions are met.

Example:
- Traffic congestion detected
- Activator rule evaluates the condition
- Automatically sends a rerouting notification or triggers a workflow

- **Real-Time Dashboards** visualize data.
- **Eventstreams** ingest and route streaming data.
- **Activator** automates responses.

---

# Question 2

### Which feature in Microsoft Fabric would you use to set up automated alerts when a specific data pattern is detected?

- A. Eventhouse
- ✅ **B. Activator**
- C. Real-Time Dashboards

## ✅ Correct Answer

**B. Activator**

### Explanation

Activator allows you to create **rules** that monitor data and send alerts or trigger automated actions.

Examples:
- Send an email when CPU usage exceeds 90%.
- Notify staff when inventory is low.
- Trigger a Power Automate flow when sales drop.

---

# Question 3

### Which component would you use to detect anomalies in streaming transaction data in real-time?

- A. Real-Time Dashboards
- ✅ **B. Eventhouse**
- C. Activator

## ✅ Correct Answer

**B. Eventhouse**

### Explanation

**Eventhouse** stores and analyzes high-volume streaming data using **Kusto Query Language (KQL)**.

It enables:
- Real-time analytics
- Pattern detection
- Trend analysis
- Anomaly detection

- **Activator** responds to detected conditions.
- **Real-Time Dashboards** display results.

---

# Question 4

### What role does the `summarize` operator play in a KQL query within Microsoft Fabric?

- ✅ **A. It aggregates data across specified columns using functions like AVG, SUM, MIN, and MAX.**
- B. It filters data based on specified conditions.
- C. It transforms data into a different structure.

## ✅ Correct Answer

**A. It aggregates data across specified columns using functions like AVG, SUM, MIN, and MAX.**

### Explanation

The **summarize** operator groups records and computes aggregate values.

Example:

```kql
Sales
| summarize TotalSales = sum(Amount) by Region
```

Other common aggregation functions include:
- `count()`
- `avg()`
- `min()`
- `max()`

---

# Question 5

### While executing a KQL query, you find that the query returns more rows than expected. Which KQL operator might you need to adjust to limit the number of rows returned?

- A. summarize
- ✅ **B. take**
- C. project

## ✅ Correct Answer

**B. take**

### Explanation

The **take** operator limits the number of rows returned.

Example:

```kql
Sales
| take 100
```

Returns only the first 100 records.

Other operators:
- **project** selects columns.
- **summarize** aggregates data.

---

# Question 6

### Which KQL operator would you use to combine data from two tables based on a shared key in Microsoft Fabric?

- ✅ **A. join**
- B. union
- C. merge

## ✅ Correct Answer

**A. join**

### Explanation

The **join** operator combines related records using a common key.

Example:

```kql
Orders
| join Customers on CustomerID
```

Comparison:

| Operator | Purpose |
|----------|---------|
| **join** | Combine related tables using a common key |
| **union** | Append rows from multiple tables |
| **merge** | Not a KQL operator |

---

# Question 7

### In designing a real-time workflow to manage inventory levels, which Activator feature should be utilized to automatically reorder stock when levels fall below a specified point?

- ✅ **A. Rules**
- B. Event transformation
- C. Data sources

## ✅ Correct Answer

**A. Rules**

### Explanation

Activator **Rules** define:

- The condition to monitor
- The action to perform

Example:

```
IF Inventory < 20
THEN Send Purchase Order
```

Rules are the core automation mechanism in Activator.

---

# Question 8

### During a review of your automated workflow in Microsoft Fabric, you identify that no actions are being triggered despite accurate data flow. Which key component might be missing?

- ✅ **A. Properly configured Activator rules**
- B. SQL-based data transformation
- C. Real-Time Dashboard visualizations

## ✅ Correct Answer

**A. Properly configured Activator rules**

### Explanation

If data is flowing correctly but no automation occurs, the most likely issue is that:

- No rule exists, or
- The rule conditions are incorrect, or
- The rule is disabled.

Without an Activator rule, no actions will be triggered.

---

# Question 9

### During a workflow review, you find that automatic responses aren't occurring despite the presence of relevant event data in Microsoft Fabric. Which component is likely misconfigured or missing?

- ✅ **A. Activator rules defining the conditions for actions**
- B. Real-time dashboard visualizations
- C. KQL queries to extract event data

## ✅ Correct Answer

**A. Activator rules defining the conditions for actions**

### Explanation

Even when event data is successfully ingested, automatic responses depend on correctly configured **Activator rules**.

These rules:
- Monitor incoming events
- Evaluate conditions
- Trigger actions such as alerts, emails, or workflows

Without them, no automated response will occur.

---

# 📚 Key Takeaways

| Concept | Remember |
|----------|----------|
| **Eventstreams** | Ingest and route real-time event data |
| **Eventhouse** | Store and analyze streaming data using KQL |
| **Activator** | Trigger automated actions based on event conditions |
| **Real-Time Dashboards** | Visualize live streaming data |
| **summarize** | Aggregate data (SUM, AVG, COUNT, MIN, MAX) |
| **take** | Limit the number of returned rows |
| **project** | Select specific columns |
| **join** | Combine tables using a shared key |
| **union** | Append rows from multiple tables |
| **Activator Rules** | Define conditions and automated actions |
