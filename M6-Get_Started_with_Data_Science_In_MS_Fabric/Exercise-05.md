# 🤖 Get Started with Data Science in Microsoft Fabric

## 📖 Overview

Microsoft Fabric provides an integrated **Data Science** experience that enables you to:

- Ingest and explore data
- Transform data using notebooks or Data Wrangler
- Train machine learning models
- Track experiments with MLflow
- Save and manage ML models

In this lab, you'll use the **Azure Open Datasets Diabetes dataset** to build both a **regression** and a **classification** model.

---

## 🎯 Objectives

In this lab, you will learn how to:

- Create a Microsoft Fabric workspace
- Create and use a notebook
- Load data into Spark
- Explore data visually
- Prepare data using Data Wrangler
- Train regression and classification models
- Track experiments using MLflow
- Save an ML model
- Stop the Spark session
- Clean up Fabric resources

---

## ⏱ Estimated Time

**20 minutes**

---

## 📋 Prerequisites

- Microsoft Fabric account
- Fabric Trial, Premium, or Paid Capacity

---

# Part 1 — Create a Workspace

1. Open Microsoft Fabric:

   https://app.fabric.microsoft.com/home?experience=fabric

2. Sign in.

3. Select **Workspaces**.

4. Create a new workspace.

Example:

```text
DataScienceLab
```

5. Under **Advanced**, choose:

- Fabric Trial
- Fabric
- Power BI Premium

6. Open the workspace.

The workspace should initially be empty.

---

# Part 2 — Create a Notebook

Select:

```text
Create
```

Under:

```text
Data Science
```

Choose:

```text
Notebook
```

Provide a unique notebook name.

A notebook opens with one code cell.

---

## Convert the First Cell to Markdown

Select the first code cell.

Click:

```text
M↓
```

Convert it to a **Markdown** cell.

Edit the cell.

Replace the contents with:

```markdown
# Data science in Microsoft Fabric
```

Run the markdown cell.

---

# Part 3 — Load the Diabetes Dataset

Create a new code cell.

Run:

```python
# Azure storage access info for open dataset diabetes
blob_account_name = "azureopendatastorage"
blob_container_name = "mlsamples"
blob_relative_path = "diabetes"
blob_sas_token = r""

# Set Spark config
wasbs_path = (
    f"wasbs://{blob_container_name}@{blob_account_name}.blob.core.windows.net/{blob_relative_path}"
)

spark.conf.set(
    f"fs.azure.sas.{blob_container_name}.{blob_account_name}.blob.core.windows.net",
    blob_sas_token,
)

print("Remote blob path:", wasbs_path)

# Load dataset
df = spark.read.parquet(wasbs_path)
```

Run the cell.

> **Note**
>
> The first Spark operation may take a minute while the Spark pool starts.

---

# Part 4 — Display the Data

Create another code cell.

Run:

```python
display(df)
```

Review the dataset.

Columns include:

- AGE
- SEX
- BMI
- BP
- S1
- S2
- S3
- S4
- S5
- S6
- Y

---

## Create a Visualization

Above the table:

Select:

```text
+ New Chart
```

Choose:

```text
Build my own
```

Settings:

| Setting | Value |
|----------|-------|
| Chart Type | Box Plot |
| Y-Axis | Y |

Review the distribution of the **Y** column.

---

# Part 5 — Convert Spark DataFrame to Pandas

Create a new code cell.

Run:

```python
df = df.toPandas()

df.head()
```

The dataset is now stored as a Pandas DataFrame.

---

# Part 6 — Prepare Data with Data Wrangler

Select:

```text
Data Wrangler
```

Choose:

```text
df
```

Wait for Data Wrangler to open.

---

## Create a Binary Risk Column

Select the:

```text
Y
```

column.

Open:

```text
Operations
→ Formulas
→ Create Column from Formula
```

Configure:

| Setting | Value |
|----------|-------|
| Column Name | Risk |
| Formula | `(df['Y'] > 211.5).astype(int)` |

Click:

```text
Apply
```

A new column named **Risk** is created.

Approximately **25%** of the rows should have a value of **1**.

---

## Generate Notebook Code

Select:

```text
Add Code to Notebook
```

Run the generated cell.

---

## Verify the Dataset

Run:

```python
df_clean.describe()
```

Review the transformed dataset.

---

# Part 7 — Train a Regression Model

Split the data.

Run:

```python
from sklearn.model_selection import train_test_split

X = df_clean[
    ['AGE','SEX','BMI','BP','S1','S2','S3','S4','S5','S6']
].values

y = df_clean['Y'].values

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.30,
    random_state=0
)
```

---

## Create an MLflow Experiment

Run:

```python
import mlflow

experiment_name = "diabetes-regression"

mlflow.set_experiment(experiment_name)
```

---

## Train the Regression Model

Run:

```python
from sklearn.linear_model import LinearRegression

with mlflow.start_run():

    mlflow.autolog()

    model = LinearRegression()

    model.fit(X_train, y_train)
```

MLflow automatically records:

- Parameters
- Metrics
- Model
- Artifacts

---

# Part 8 — Train a Classification Model

Split the data using the **Risk** label.

Run:

```python
from sklearn.model_selection import train_test_split

X = df_clean[
    ['AGE','SEX','BMI','BP','S1','S2','S3','S4','S5','S6']
].values

y = df_clean['Risk'].values

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.30,
    random_state=0
)
```

---

## Create Another Experiment

Run:

```python
import mlflow

experiment_name = "diabetes-classification"

mlflow.set_experiment(experiment_name)
```

---

## Train the Classification Model

Run:

```python
from sklearn.linear_model import LogisticRegression

with mlflow.start_run():

    mlflow.sklearn.autolog()

    model = LogisticRegression(
        C=1/0.1,
        solver="liblinear"
    ).fit(X_train, y_train)
```

MLflow automatically logs the training process.

---

# Part 9 — Explore MLflow Experiments

Return to your workspace.

Open:

```text
diabetes-regression
```

Review:

- Run Metrics
- Parameters
- Artifacts

Refresh the page if no runs appear.

Next, open:

```text
diabetes-classification
```

Compare the metrics.

Notice that classification and regression models use different evaluation metrics.

---

# Part 10 — Save the Best Model

Inside the experiment:

Select:

```text
Save as ML Model
```

Choose:

```text
Create New ML Model
```

Select a model folder.

Model name:

```text
model-diabetes
```

Click:

```text
Save
```

Open the saved model.

Notice the relationships between:

- ML Model
- Experiment
- Experiment Run

---

# Part 11 — Save the Notebook

Open:

```text
Notebook Settings
```

Rename the notebook:

```text
Train and compare models
```

Save the notebook.

---

# Part 12 — Stop the Spark Session

From the notebook toolbar:

Select:

```text
Stop Session
```

This releases the Spark compute resources.

---

# Part 13 — Clean Up Resources

Delete the workspace.

Open:

```text
Workspace Settings
```

Navigate to:

```text
General
```

Select:

```text
Remove this Workspace
```

Confirm deletion.

---

# ✅ Summary

In this exercise, you learned how to:

- Create a Microsoft Fabric notebook
- Load data from Azure Open Datasets
- Explore data visually
- Transform data using Data Wrangler
- Create a binary classification label
- Train regression and classification models
- Track experiments using MLflow
- Save machine learning models
- Stop the Spark session
- Clean up Microsoft Fabric resources
