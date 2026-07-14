# Train and Score Models with Microsoft Fabric

## Overview
After ingesting, exploring, and preprocessing data, the next step is to train machine learning models. Since model development is iterative, Microsoft Fabric integrates with **MLflow** to track experiments, compare results, and manage trained models.

---

# MLflow Integration

Microsoft Fabric uses **MLflow** to:

- Track machine learning experiments.
- Log parameters, metrics, and artifacts.
- Compare multiple model runs.
- Reproduce experiments.
- Register and version trained models.

---

# Experiments

An **Experiment** is a collection of related model training runs.

## Experiment Run

A **Run** represents one execution of model training.

Example:
- Train the same forecasting model using different datasets.
- Each training execution becomes a separate run.
- Compare all runs to identify the best-performing model.

---

# Track Model Performance

Each experiment run can log:

## Parameters
Model configuration values, such as:
- Learning rate
- Number of trees
- Dataset version
- Hyperparameters

## Metrics
Performance measurements, such as:
- Accuracy
- Precision
- Recall
- RMSE
- MAE
- F1 Score

## Artifacts
Files produced during training, including:
- Trained model
- Plots
- Evaluation reports
- Feature importance charts

---

# Experiment Comparison

Fabric provides an experiment dashboard where you can:

- View all experiment runs.
- Compare metrics across runs.
- Inspect run details.
- Identify the best model configuration.

Benefits:
- Easier experimentation
- Better reproducibility
- Simplified model selection

---

# Models

After training, model artifacts can be registered as a **Model** in Microsoft Fabric.

Benefits include:

- Centralized model management
- Model versioning
- Easier deployment
- Reusable across projects

Whenever a model is saved with the same name:

- A **new version** is automatically created.
- Previous versions remain available.

---

# Generate Predictions (Scoring)

After registering a model, use it to generate predictions on new data.

Microsoft Fabric provides the:

## `PREDICT` Function

The **PREDICT** function integrates directly with MLflow models to perform **batch predictions**.

Typical workflow:

1. Receive new data.
2. Load data into Fabric.
3. Call the `PREDICT` function.
4. Generate predictions.
5. Save prediction results back to a Lakehouse table.

---

# Example Use Case

### Sales Forecasting

Weekly workflow:

1. Collect new weekly sales data.
2. Use a previously trained forecasting model.
3. Execute the `PREDICT` function.
4. Forecast next week's sales.
5. Store forecast results in a Lakehouse table.

---

# Key Components

| Component | Purpose |
|-----------|---------|
| MLflow | Track experiments and models |
| Experiment | Collection of training runs |
| Run | Single model training execution |
| Parameters | Model configuration values |
| Metrics | Performance measurements |
| Artifacts | Generated files (models, charts, reports) |
| Registered Model | Stored and versioned ML model |
| PREDICT | Generate batch predictions using registered models |

---

# Key Takeaways

- Microsoft Fabric integrates **MLflow** for experiment tracking.
- Experiments contain multiple training runs.
- Track **parameters, metrics, and artifacts** for every run.
- Compare experiment results to identify the best model.
- Register trained models for version management.
- Use the **PREDICT** function to generate batch predictions.
- Prediction results can be stored directly in a **Lakehouse** for analytics and reporting.
