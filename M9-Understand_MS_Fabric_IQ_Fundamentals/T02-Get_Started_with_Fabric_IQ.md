# Get started with Fabric IQ

## Overview

**Fabric IQ** is a workload in **Microsoft Fabric** for creating **ontologies** that define your organization's business vocabulary.

It works alongside other Fabric workloads such as:

- Data Engineering
- Data Factory
- Data Science
- Data Warehouse
- Real-Time Intelligence
- Power BI

Within the Fabric IQ workload, you create **Ontology** items (Fabric artifacts) that contain ontology definitions and data bindings.

---

# What is an Ontology?

An **ontology** is a shared business vocabulary.

It describes:

- Business entities (entity types)
- Facts about those entities (properties)
- Relationships between entities

### Example

| Entity | Properties | Relationships |
|---------|------------|---------------|
| Patient | Name, DOB, Admission Date | Assigned to Room |
| Room | Room Number, Bed Count | Located in Department |
| Department | Name, Floor | Contains Rooms |

---

# Ontology as a Business Context Layer

An ontology provides:

- Catalog of business concepts
  - Hospital
  - Patient
  - Department
  - Room
- Properties and relationships
- Data bindings to:
  - Lakehouse tables
  - Eventhouse streams
- Graph representation for navigation
- Business-level query surface

Instead of writing SQL against tables, users interact with familiar business concepts.

---

# Purpose of Fabric IQ

Fabric IQ enables organizations to:

- Model business concepts instead of database structures
- Query using business language
- Build federated queries across multiple data sources
- Support AI agents with business context
- Explore relationships visually using Graph

---

# How Fabric IQ Fits into Microsoft Fabric

## 1. Ingest and Store

Fabric IQ works with existing data stored in:

- Lakehouse tables
- Eventhouse streams

It **does not duplicate or move data**.

Instead, it creates a semantic layer over existing sources.

---

## 2. Model Business Semantics

Ontology items define:

- Entity Types
- Properties
- Relationship Types

Ontology structures can be:

- Generated automatically from Power BI semantic models
- Built manually from scratch

---

## 3. Analyze and Visualize

Fabric IQ integrates with:

- Graph in Microsoft Fabric
- Data Agents

Benefits include:

- Visual graph exploration
- Natural language querying
- Business-aware AI interactions

---

# Creating an Ontology

Navigate to:

```
Workspace
    ↓
+ New Item
    ↓
Ontology (Preview)
```

Then:

1. Enter an ontology name
2. Use:
   - Letters
   - Numbers
   - Underscores (_)
3. Do **not** use:
   - Spaces
   - Dashes (-)
4. Select **Create**

---

# Prerequisites

Fabric administrators must enable the required **tenant settings** before users can create ontology items.

---

# Ontology Interface

The ontology contains two major views.

---

## 1. Configuration Canvas

Used to design the ontology.

Create:

- Entity Types
- Properties
- Relationships

### Example

```
Patient
 ├── FirstName
 ├── LastName
 ├── DateOfBirth
 └── AdmissionDate
```

Relationships:

```
Department
      │
contains
      │
Room
      │
assigned to
      │
Patient
```

---

## 2. Preview Experience

Shows instantiated data.

Features include:

- Entity instances
- Relationship graphs
- Business-language queries
- Graph visualization
- Query Builder

---

# Build → Bind → Query Workflow

Fabric IQ follows three major steps.

---

## Step 1 — Build

Define business vocabulary.

Create:

- Entity Types
- Properties
- Relationships

### Healthcare Example

Entities:

- Patient
- Room
- Department

Properties:

- Name
- Date of Birth
- Admission Date

Relationships:

- Patient assigned to Room
- Room belongs to Department

---

## Step 2 — Bind

Connect ontology definitions to data sources.

Possible sources include:

### Lakehouse

Static data

Examples:

- Patient records
- Hospital information
- Room assignments

### Eventhouse

Streaming data

Examples:

- Vital signs
- Medical device telemetry
- Sensor readings

Bindings map source columns to ontology properties.

---

## Step 3 — Query

Once bound, users interact using business concepts.

Available experiences:

- Graph in Microsoft Fabric
- Query Builder
- AI Data Agents

No SQL is required.

---

# Separation of Concerns

Fabric IQ separates:

**Business Meaning**

from

**Physical Data Storage**

Business users work with concepts instead of tables.

---

# Connection to OneLake

Fabric IQ references existing OneLake data.

It does **not** copy data.

## Lakehouse stores

- Patient records
- Hospital data
- Room assignments

## Eventhouse stores

- Vital signs
- Sensor streams
- Time-series telemetry

---

# Federated Query Engine

Fabric IQ automatically chooses the most appropriate query engine.

| Query Type | Engine |
|------------|---------|
| Graph traversal | GQL |
| Time-series analysis | KQL |
| Business queries | Federated across sources |

Users do not need to know where data resides.

---

# Two Ways to Create an Ontology

## Option 1 — Generate from Power BI Semantic Model

Automatically creates:

- Entity Types
- Properties
- Relationships

based on:

- Tables
- Columns
- Existing model relationships

After generation, refine by:

- Renaming entities
- Verifying keys
- Updating bindings
- Adding Eventhouse streams

---

## Option 2 — Build from OneLake Data

Create everything manually.

Define:

- Entity Types
- Properties
- Relationships

Provides maximum flexibility and control.

---

# Summary

Fabric IQ enables organizations to model business knowledge independently of physical data storage.

## Key Capabilities

- Create business ontologies
- Build semantic business vocabulary
- Bind ontology to OneLake data
- Support Graph exploration
- Enable AI-powered natural language querying
- Federate queries across Lakehouse and Eventhouse
- Generate ontologies from Power BI semantic models
- Build ontologies manually from OneLake

---

# Workflow Summary

```text
OneLake Data
      │
      ▼
Build Ontology
(Entity Types, Properties, Relationships)
      │
      ▼
Bind Data Sources
(Lakehouse + Eventhouse)
      │
      ▼
Query
 ├── Graph
 ├── Query Builder
 └── AI Data Agents
```
