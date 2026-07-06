# 📘 Secure and Monitor a Warehouse

## 🎯 Overview

Security and monitoring are essential for managing a Microsoft Fabric Data Warehouse.

Fabric provides multiple layers of security to protect warehouse data while allowing controlled collaboration. It also includes monitoring tools to analyze query performance, identify bottlenecks, and optimize warehouse usage.

---

# 🔐 Security in Microsoft Fabric

Fabric implements **layered security**, allowing administrators to control access from the workspace level down to individual rows and columns.

Security is enforced regardless of whether data is accessed through:

- T-SQL
- Power BI
- Copilot
- Fabric IQ
- Other Fabric workloads

---

# 🏢 Workspace Roles

Workspace roles provide the **first layer of access control**.

Assign users based on the level of access they require.

| Role | Access |
|------|--------|
| **Admin** | Full control of the workspace and all items |
| **Member** | Create, edit, and manage content |
| **Contributor** | Create and modify content with limited administrative capabilities |
| **Viewer** | View content only; cannot modify items |

Workspace roles control access to all resources within a workspace.

---

# 📂 Item Permissions

When you want to share a specific warehouse instead of the entire workspace, use **Item Permissions**.

This provides more granular access control.

## Available Permissions

### Read

Allows users to connect to the warehouse using the SQL endpoint.

**Required** for SQL connections.

---

### ReadData

Allows users to read data from:

- Tables
- Views

---

### ReadAll

Allows users to access the underlying **Parquet files** stored in OneLake.

---

## Important

A user **must have at least the `Read` permission** to connect to the SQL Analytics Endpoint.

---

# 🛡️ Granular SQL Security

Fabric supports fine-grained security using standard **T-SQL** features.

---

## 1. Object-Level Security

Controls access to specific database objects such as:

- Tables
- Views
- Stored Procedures

---

## 2. Row-Level Security (RLS)

Restricts which rows a user can view.

Implemented using **WHERE clause predicates**.

### Example

A regional manager only sees sales for their assigned region.

---

## 3. Column-Level Security (CLS)

Restricts visibility of specific columns.

Example:

Hide:

- Salary
- Credit Card Number
- Social Security Number

while allowing access to the rest of the table.

---

## 4. Dynamic Data Masking (DDM)

Masks sensitive information for non-privileged users.

Examples:

- Email addresses
- Phone numbers
- Account numbers
- Personal information

The actual data remains unchanged.

---

# 🤖 Security and AI

Security policies also apply to AI-powered features.

This includes:

- Copilot
- Fabric IQ
- Data Agents

AI can only access data that users are authorized to see.

This helps maintain:

- Data governance
- Compliance
- Privacy

---

# 📊 Monitoring a Warehouse

Monitoring helps administrators:

- Detect slow queries
- Optimize performance
- Understand warehouse usage
- Identify resource-intensive workloads

---

# 📈 Query Insights

**Query Insights** stores historical SQL execution information.

### Data Retention

- **30 days**

---

## Benefits

- Find long-running queries
- Track performance trends
- Identify expensive queries
- Optimize workloads

---

## Query Insights System Views

| View | Purpose |
|------|---------|
| `queryinsights.exec_requests_history` | History of completed SQL requests |
| `queryinsights.long_running_queries` | Longest-running queries |
| `queryinsights.exec_sessions_history` | Completed SQL sessions |

---

# ⚡ Dynamic Management Views (DMVs)

DMVs provide **real-time** monitoring information.

They display:

- Active sessions
- Running queries
- Current requests
- Resource usage

---

## Example DMV

```sql
sys.dm_exec_requests
```

This DMV displays:

- Request ID
- Session ID
- Start Time
- Execution Time
- Running Status

Useful for identifying queries that are currently consuming resources.

---

# 🛑 Terminating Queries

Administrators can stop long-running queries using the **KILL** command.

## Permission Required

Only **Workspace Admins** can execute:

```sql
KILL
```

Other users:

- Can monitor their own sessions.
- Cannot terminate other users' queries.

---

# 🔄 Security & Monitoring Workflow

```text
Users
   │
   ▼
Workspace Roles
   │
   ▼
Item Permissions
   │
   ▼
SQL Security
(RLS, CLS, DDM)
   │
   ▼
Warehouse Access
   │
   ▼
Copilot / Power BI / SQL
   │
   ▼
Query Insights
   │
   ▼
DMVs
   │
   ▼
Performance Monitoring
```

---

# 📝 Key Takeaways

- Microsoft Fabric uses **layered security** to protect warehouse data.
- **Workspace Roles** provide the first level of access control.
- **Item Permissions** allow sharing individual warehouses without exposing the entire workspace.
- SQL connections require at least the **Read** permission.
- Fabric supports:
  - Object-Level Security
  - Row-Level Security (RLS)
  - Column-Level Security (CLS)
  - Dynamic Data Masking (DDM)
- Security policies are enforced across **Power BI**, **Copilot**, **Fabric IQ**, and all SQL access methods.
- **Query Insights** stores **30 days** of historical query performance data.
- **Dynamic Management Views (DMVs)** provide real-time monitoring of active sessions and queries.
- Only **Workspace Admins** can terminate running queries using the **KILL** command.

---

# 📌 Important Terms

| Term | Description |
|--------|-------------|
| Workspace Role | First layer of access control within a Fabric workspace |
| Item Permission | Permissions assigned to individual warehouse items |
| Read | Permission required to connect through the SQL Analytics Endpoint |
| ReadData | Permission to read tables and views |
| ReadAll | Permission to access underlying OneLake Parquet files |
| Object-Level Security | Restricts access to tables, views, or stored procedures |
| Row-Level Security (RLS) | Restricts visible rows based on user permissions |
| Column-Level Security (CLS) | Restricts access to specific columns |
| Dynamic Data Masking (DDM) | Masks sensitive values for unauthorized users |
| Query Insights | Historical SQL performance monitoring tool (30-day retention) |
| Dynamic Management Views (DMVs) | Real-time monitoring views for active SQL sessions and queries |
| `sys.dm_exec_requests` | DMV that displays currently running SQL requests |
| KILL | SQL command used by Workspace Admins to terminate running sessions |
| Copilot | AI assistant that respects all Fabric security policies |
| Fabric IQ | AI capability that operates within defined warehouse security boundaries |
