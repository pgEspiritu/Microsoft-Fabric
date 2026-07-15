# Explore Copilot for SQL Database in Microsoft Fabric

## Overview

**Copilot for SQL Database** is an AI-powered assistant integrated into **Microsoft Fabric SQL Database** that helps users write, understand, troubleshoot, and optimize T-SQL queries.

By leveraging **Natural Language to SQL**, intelligent code completion, and query assistance, Copilot makes database development faster and more accessible.

> **Note:** Copilot is **schema-aware** but **does not use table data** to generate T-SQL suggestions.

---

# Key Capabilities

- Natural Language to SQL conversion
- Intelligent T-SQL code generation
- Automatic code completion
- Query explanation
- Query error correction
- AI-assisted troubleshooting

---

# Natural Language to SQL

Copilot can translate plain English questions into T-SQL queries.

Example prompts:

- Which employees have completed more than two projects this quarter?
- List all products that were out of stock last month.
- Rank each department by employee satisfaction score.
- Create a primary key constraint named `PK_Product_ProductID` on the `ProductID` column.

This allows users to interact with databases without manually writing complex SQL.

---

# Schema-Aware Assistance

Copilot understands your database schema, including:

- Tables
- Columns
- Relationships
- Database objects

This enables it to generate SQL queries that align with your database structure.

> **Important:** Copilot **does not access or analyze the actual data stored in tables** when generating SQL suggestions.

---

# Code Completion

While writing T-SQL, Copilot provides:

- Intelligent code suggestions
- SQL syntax completion
- Faster query authoring
- Reduced typing effort

---

# Quick Actions

The SQL query editor includes built-in AI actions.

## Explain

- Explains what a SQL query does.
- Helps users understand unfamiliar SQL code.
- Useful for learning and reviewing queries.

## Fix

- Detects SQL errors.
- Suggests corrections.
- Automatically helps resolve syntax and logic issues.

---

# Chat Pane

The **Copilot Chat Pane** allows users to interact using natural language.

You can:

- Ask database questions.
- Generate SQL queries.
- Request query explanations.
- Troubleshoot SQL errors.
- Receive development guidance.

---

# Access Copilot

To use Copilot in Microsoft Fabric:

1. Open your **SQL Database**.
2. Select the **Copilot** button in the ribbon to open the chat pane.

Or use the Query Editor toolbar:

- **Explain**
- **Fix**

---

# Benefits

- Faster SQL development
- Easier query writing
- Simplified troubleshooting
- Improved productivity
- Lower learning curve for SQL
- Better understanding of complex queries

---

# Copilot Features Summary

| Feature | Purpose |
|---------|---------|
| Chat Pane | Ask questions and generate T-SQL using natural language |
| Natural Language to SQL | Convert plain English into SQL queries |
| Code Completion | Suggest SQL code while typing |
| Explain | Describe what a SQL query does |
| Fix | Detect and correct SQL query errors |
| Schema Awareness | Generate SQL based on database structure |

---

# Key Takeaways

- **Copilot for SQL Database** is an AI assistant integrated into Microsoft Fabric.
- Supports **Natural Language to SQL** for easier query creation.
- Provides **schema-aware** SQL generation.
- Includes **Code Completion**, **Explain**, and **Fix** features.
- Helps improve SQL development, troubleshooting, and learning.
- **Copilot does not use table data** when generating SQL suggestions—it relies only on the database schema.
