# 📘 Understand the Data Science Process

## 🎯 Overview

Data science goes beyond creating visualizations—it involves discovering hidden patterns in data and using those patterns to make predictions through **machine learning (ML)**.

A typical data science project follows a structured workflow, from defining the business problem to generating actionable insights.

---

# 🤖 What is Machine Learning?

**Machine Learning (ML)** is a branch of Artificial Intelligence (AI) that trains models to recognize patterns in data.

Once trained, these models can make predictions or automate decision-making.

### Example

Use historical sales data to predict how many products will be sold next week.

---

# 📚 Common Types of Machine Learning Models

Choosing the right model depends on the business problem and the available data.

## 1. Classification

Predicts a **categorical** value.

### Examples

- Will a customer churn?
- Is an email spam or not?
- Is a transaction fraudulent?

**Output:** Categories (Yes/No, Class A/B/C)

---

## 2. Regression

Predicts a **numerical** value.

### Examples

- Product price
- House value
- Sales amount

**Output:** Continuous numeric value

---

## 3. Clustering

Groups similar records together without predefined labels.

### Examples

- Customer segmentation
- Product grouping
- Market segmentation

**Output:** Clusters or groups

---

## 4. Forecasting

Predicts future values using **time-series** data.

### Examples

- Monthly sales
- Inventory demand
- Weather prediction

**Output:** Future numerical values over time

---

# 🔄 Data Science Process

A typical data science project follows these stages:

```text
Define the Problem
        │
        ▼
Get the Data
        │
        ▼
Prepare the Data
        │
        ▼
Train the Model
        │
        ▼
Generate Insights
```

---

# 1️⃣ Define the Problem

Work with business stakeholders to determine:

- What problem needs to be solved?
- What should the model predict?
- How will success be measured?

### Example

Predict customer churn with at least **90% accuracy**.

---

# 2️⃣ Get the Data

Collect and organize the required data.

In Microsoft Fabric:

- Store data in a **Lakehouse**
- Connect to multiple data sources
- Centralize data for analysis

---

# 3️⃣ Prepare the Data

Most of a data scientist's time is spent preparing data.

Common tasks include:

- Explore the data
- Remove missing values
- Clean inconsistent records
- Transform data
- Engineer new features
- Select useful variables

In Fabric, data is commonly read from a **Lakehouse** into a **Notebook** for processing.

---

# 4️⃣ Train the Model

Choose:

- A machine learning algorithm
- Hyperparameter values

Then train the model using the prepared dataset.

Training often requires experimenting with different algorithms until the best-performing model is found.

---

# 5️⃣ Generate Insights

Once the model is trained:

- Make predictions
- Perform batch scoring
- Deliver insights to support business decisions

Examples:

- Sales forecasts
- Customer churn predictions
- Product recommendations

---

# 🧪 Experiment Tracking with MLflow

Training multiple models requires keeping track of experiments.

Microsoft Fabric integrates **MLflow** to manage machine learning experiments.

MLflow helps you:

- Track model runs
- Compare experiments
- Record hyperparameters
- Monitor evaluation metrics
- Save trained models
- Deploy successful models

---

# 🐍 Common Python Libraries

Data scientists commonly use open-source libraries for preparing data and training models.

## Data Preparation

- **Pandas**
- **NumPy**

## Machine Learning

- **Scikit-Learn**
- **PyTorch**
- **SynapseML**

---

# ⏱ Where Data Scientists Spend Most Time

The majority of a data science project is spent on:

- Data preparation
- Model training
- Experimentation

The quality of the data and the selected algorithm have the greatest impact on model performance.

---

# 🔄 Data Science Workflow in Microsoft Fabric

```text
Business Problem
        │
        ▼
Lakehouse
(Store Data)
        │
        ▼
Notebook
(Prepare Data)
        │
        ▼
Machine Learning
(Train Model)
        │
        ▼
MLflow
(Track Experiments)
        │
        ▼
Predictions
(Generate Insights)
```

---

# 📝 Key Takeaways

- Machine learning discovers patterns in data to make predictions.
- The four common machine learning model types are:
  - **Classification** (categorical prediction)
  - **Regression** (numerical prediction)
  - **Clustering** (group similar records)
  - **Forecasting** (predict future values)
- A typical data science process includes:
  1. Define the problem
  2. Get the data
  3. Prepare the data
  4. Train the model
  5. Generate insights
- Most effort is spent preparing data and training models.
- Microsoft Fabric stores data in **Lakehouses** and uses **Notebooks** for data preparation and model development.
- **MLflow** tracks experiments, compares models, and simplifies model deployment.
- Common Python libraries include:
  - **Pandas**
  - **NumPy**
  - **Scikit-Learn**
  - **PyTorch**
  - **SynapseML**

---

# 📖 Important Terms

| Term | Description |
|------|-------------|
| Machine Learning (ML) | AI technique that learns patterns from data to make predictions |
| Classification | Predicts categorical outcomes |
| Regression | Predicts numerical values |
| Clustering | Groups similar records without predefined labels |
| Forecasting | Predicts future values using time-series data |
| Lakehouse | Central storage used for analytics and machine learning data |
| Notebook | Interactive environment for data preparation and model development |
| Hyperparameter | Configuration value that controls how a machine learning algorithm learns |
| MLflow | Platform for tracking machine learning experiments and managing models |
| Batch Scoring | Using a trained model to generate predictions for a large dataset |
| Pandas | Python library for data manipulation |
| NumPy | Python library for numerical computing |
| Scikit-Learn | Python machine learning library |
| PyTorch | Deep learning framework |
| SynapseML | Microsoft machine learning library for Apache Spark |
