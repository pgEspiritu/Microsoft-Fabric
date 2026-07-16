# Secure Databases in Microsoft Fabric

## Overview

Microsoft Fabric SQL Database provides **built-in security features** to protect sensitive data at both the **database** and **SQL analytics endpoint** levels.

Security controls ensure that only authorized users can access or view sensitive information without requiring changes to existing applications.

---

# Security Capabilities

SQL Database in Microsoft Fabric uses the same **SQL engine** as Azure SQL Database, allowing users to leverage familiar **T-SQL-based security features**.

Benefits include:

- Fine-grained access control
- Protection of sensitive data
- Secure data sharing
- Enterprise-grade database security

---

# Workspace Roles

Workspace roles control access to items within a Fabric workspace.

Available roles include:

- **Admin** – Full control over the workspace.
- **Member** – Can manage and edit workspace content.
- **Contributor** – Can create and modify content.
- **Viewer** – Read-only access.

Workspace roles help maintain security while supporting collaboration.

---

# Item Permissions

Permissions can also be assigned directly to individual SQL databases.

Purpose:

- Share specific SQL databases without granting access to the entire workspace.
- Enable downstream consumption securely.

You can manage permissions for:

- SQL Database
- SQL Analytics Endpoint
- Default Semantic Model

**Location:**

Workspace → Select Item → **Manage Permissions**

> **Note:**  
> Item permissions do **not** modify the security metadata defined inside the database.

---

# Data Protection Features

For more granular security, SQL Database supports **T-SQL-based security controls**.

## Object-Level Security (OLS)

Controls access to specific database objects, such as:

- Tables
- Views
- Stored Procedures

---

## Column-Level Security (CLS)

Restricts access to selected columns within a table.

Example:

- Hide salary columns
- Restrict personal information

---

## Row-Level Security (RLS)

Restricts which rows users can view using **WHERE** clause filters.

Example:

- Employees only see records from their assigned region.
- Managers see only their department's data.

---

## Dynamic Data Masking (DDM)

Masks sensitive information for unauthorized users.

Common examples:

- Email addresses
- Phone numbers
- Credit card numbers
- Personal identifiers

Masking occurs automatically without modifying the stored data.

---

# Manage SQL Security

Database security can be managed directly in the Fabric portal.

**Navigation:**

1. Open the SQL Database.
2. Select **Security**.
3. Choose **Manage SQL Security**.

From there, administrators can configure:

- Database roles
- User permissions
- Security policies
- Data protection settings

---

# Security Layers

| Security Layer | Purpose |
|----------------|---------|
| Workspace Roles | Control workspace-level access |
| Item Permissions | Share individual SQL databases |
| Object-Level Security | Restrict access to database objects |
| Column-Level Security | Protect sensitive columns |
| Row-Level Security | Filter visible rows per user |
| Dynamic Data Masking | Hide sensitive data from unauthorized users |

---

# Key Takeaways

- SQL Database in Fabric provides **enterprise-grade security** using the SQL Server engine.
- **Workspace roles** manage overall access to Fabric resources.
- **Item permissions** allow secure sharing of individual databases.
- **T-SQL security features** provide granular control over data access.
- Supported protections include:
  - Object-Level Security (OLS)
  - Column-Level Security (CLS)
  - Row-Level Security (RLS)
  - Dynamic Data Masking (DDM)
- SQL security settings can be managed directly through the **Fabric portal**.
