# 📘 Explore and Process Data with Microsoft Fabric

## 🎯 Overview

Data is the foundation of every data science project. The success of a machine learning model depends on both the **quantity** and **quality** of the data used for training.

Microsoft Fabric provides powerful tools to:

- Ingest data from multiple sources
- Store data centrally
- Explore and analyze data
- Clean and transform data
- Prepare datasets for machine learning

Fabric supports both **low-code** and **code-first** approaches for data ingestion and transformation.

---

# 📥 Ingest Data into Microsoft Fabric

Before analyzing data, it must first be imported into Microsoft Fabric.

## Supported Data Sources

Data can be ingested from:

- Local files (CSV, Excel, etc.)
- Azure Data Lake Storage Gen2
- Cloud storage
- Other supported external data sources

---

# 🏠 Store Data in a Lakehouse

After ingestion, data is typically stored in a **Microsoft Fabric Lakehouse**.

A Lakehouse acts as a centralized repository for:

- Structured data
- Semi-structured data
- Unstructured data

Using a Lakehouse allows data to be easily reused for analytics, reporting, and machine learning.

---

# 🔄 Data Ingestion Workflow

```text
Data Sources
(Local / Cloud)
        │
        ▼
Data Ingestion
        │
        ▼
Lakehouse
(Central Storage)
        │
        ▼
Notebook / Data Wrangler
        │
        ▼
Processed Data
        │
        ▼
Machine Learning
```

---

# 📒 Explore and Transform Data with Notebooks

Microsoft Fabric provides **Notebooks** for interactive data exploration and processing.

Notebooks are powered by **Apache Spark**, enabling large-scale distributed data processing.

---

# ⚡ Apache Spark

**Apache Spark** is an open-source framework for:

- Large-scale data processing
- Data analytics
- Machine learning
- Distributed computing

Spark enables fast processing of large datasets across multiple computing resources.

---

# 🔥 Spark Sessions

When using a notebook:

- A **Spark session** automatically starts when the first cell is executed.
- The session remains active while you continue working.
- After a period of inactivity, the session automatically stops to reduce costs.
- Users can also stop the session manually.

---

# 💻 Supported Notebook Languages

For data science workloads, Microsoft Fabric supports:

- **PySpark (Python)**
- **SparkR (R)**

These languages allow users to analyze, transform, and prepare data using familiar programming environments.

---

# 📊 Explore Data

Within a notebook, data scientists can:

- Read data from a Lakehouse
- Explore datasets
- Analyze statistics
- Create visualizations
- Identify data quality issues

Built-in visualization tools help quickly understand data distributions and patterns.

---

# 🔄 Transform Data

Common transformation tasks include:

- Cleaning data
- Filtering records
- Creating calculated columns
- Aggregating data
- Reshaping datasets
- Feature engineering

After transformation, the processed data can be written back to the Lakehouse for future use.

---

# 🧹 Prepare Data with Data Wrangler

Microsoft Fabric includes **Data Wrangler**, a low-code tool for exploring and cleaning data.

It simplifies data preparation without requiring extensive programming.

---

# 📈 Data Wrangler Features

## Data Overview

Provides a descriptive summary of the dataset, including:

- Column information
- Data types
- Summary statistics

---

## Data Quality Checks

Helps identify issues such as:

- Missing values
- Invalid data
- Outliers
- Data inconsistencies

---

## Built-in Cleaning Operations

Examples include:

- Remove missing values
- Replace values
- Rename columns
- Filter rows
- Change data types
- Other common data-cleaning tasks

---

## Automatic Code Generation

One of Data Wrangler's most useful features is automatic code generation.

When a cleaning operation is selected:

1. A preview of the transformed data is displayed.
2. The corresponding code is automatically generated.
3. The generated code can be exported and executed.

This helps users learn coding while accelerating data preparation.

---

# 🔄 Data Preparation Workflow

```text
Load Data
      │
      ▼
Explore Dataset
      │
      ▼
Identify Data Issues
      │
      ▼
Apply Cleaning Operations
      │
      ▼
Generate Code
      │
      ▼
Save Clean Data
      │
      ▼
Machine Learning
```

---

# 🤖 Role in Data Science

Microsoft Fabric provides multiple tools that support the data preparation stage of the data science lifecycle:

- **Lakehouse** → Centralized data storage
- **Notebooks** → Code-first exploration and transformation
- **Apache Spark** → Large-scale data processing
- **Data Wrangler** → Low-code data cleaning and transformation

These tools help create high-quality datasets for training machine learning models.

---

# 📝 Key Takeaways

- High-quality data is essential for successful machine learning models.
- Microsoft Fabric supports both **low-code** and **code-first** approaches to data preparation.
- Data can be ingested from local files, Azure Data Lake Storage Gen2, and other cloud sources.
- A **Lakehouse** serves as the centralized repository for structured, semi-structured, and unstructured data.
- **Notebooks** provide an interactive environment for data exploration and transformation.
- **Apache Spark** powers notebook execution and large-scale distributed data processing.
- Spark sessions start automatically when notebook cells are executed and stop after inactivity to optimize costs.
- Supported notebook languages include **PySpark** and **SparkR**.
- **Data Wrangler** simplifies data exploration and cleaning with built-in operations and automatic code generation.
- Cleaned and transformed data can be saved back to the Lakehouse for analytics and machine learning.

---

# 📖 Important Terms

| Term | Description |
|------|-------------|
| Data Ingestion | Process of importing data into Microsoft Fabric |
| Lakehouse | Centralized storage for structured, semi-structured, and unstructured data |
| Notebook | Interactive environment for exploring and transforming data |
| Apache Spark | Distributed framework for large-scale data processing |
| Spark Session | Temporary compute environment used to execute notebook code |
| PySpark | Python API for Apache Spark |
| SparkR | R API for Apache Spark |
| Data Wrangler | Low-code tool for exploring, cleaning, and transforming data |
| Data Transformation | Process of cleaning, reshaping, and preparing data for analysis or machine learning |
| Summary Statistics | Statistical overview of a dataset used to assess data quality |
| Code Generation | Automatic creation of executable code based on selected Data Wrangler operations |
