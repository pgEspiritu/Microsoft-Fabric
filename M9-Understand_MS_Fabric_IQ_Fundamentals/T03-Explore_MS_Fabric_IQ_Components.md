# Explore Microsoft Fabric IQ Components

## Overview

Microsoft Fabric IQ consists of several integrated components that work together to define, query, analyze, and visualize business data.

### Core Components

1. Ontology Items
2. Data Agents
3. Graph in Microsoft Fabric
4. Power BI Semantic Models

Together, these components enable business users to interact with data using business concepts instead of technical database structures.

---

# Fabric IQ Architecture

```text
                   Microsoft Fabric IQ

        ┌─────────────────────────────────┐
        │         Ontology Item           │
        │ Business Vocabulary & Semantics │
        └───────────────┬─────────────────┘
                        │
         ┌──────────────┼──────────────┐
         │              │              │
         ▼              ▼              ▼
   Data Agents      Graph          Semantic Model
Natural Language  Visualization   Ontology Generation
     Queries      & Traversal
```

---

# 1. Ontology Items

## Purpose

An **Ontology Item** defines your organization's shared business vocabulary.

It describes:

- Business entities
- Entity properties
- Relationships
- Data bindings to OneLake

Instead of exposing tables and columns, it exposes business concepts.

---

## Example

Healthcare ontology:

### Entity Types

- Hospital
- Department
- Room
- Patient
- VitalSign

### Properties

Hospital

- HospitalID
- HospitalName

Department

- DepartmentName

Room

- RoomNumber

Patient

- PatientID
- Name
- AdmissionDate

VitalSign

- HeartRate
- BloodPressure

---

## Relationships

```
Hospital
     │
contains
     ▼
Department
     │
contains
     ▼
Room
     │
occupied by
     ▼
Patient
     │
has
     ▼
VitalSign
```

---

## Data Binding

Ontology concepts are bound to actual OneLake data.

Example:

| Business Concept | Data Source |
|------------------|------------|
| Patient | Lakehouse Table |
| Department | Lakehouse Table |
| Room | Lakehouse Table |
| VitalSign | Eventhouse Stream |

---

## Benefits

- Shared business vocabulary
- Business-friendly querying
- AI understanding
- Graph visualization
- Cross-source integration

---

# 2. Data Agents

## Purpose

A **Fabric Data Agent** is a conversational AI assistant that answers questions using natural language.

It is powered by:

- Azure OpenAI Assistant APIs

---

## Supported Data Sources

A data agent can connect to up to **five** data sources.

Supported sources include:

- Lakehouse
- Warehouse
- KQL Database
- Power BI Semantic Model
- Ontology

---

## How Data Agents Work

```text
User Question
      │
      ▼
Natural Language Processing
      │
      ▼
Determine Best Data Source
      │
      ▼
Generate Appropriate Query
      │
      ▼
Return Answer
```

---

## Query Language Generated

| Data Source | Generated Query |
|-------------|----------------|
| Lakehouse | SQL |
| Warehouse | SQL |
| Semantic Model | DAX |
| KQL Database | KQL |
| Ontology | Business Concept Queries |

---

## Healthcare Example

Question:

> Which patients in cardiology have elevated heart rates right now?

The data agent automatically:

1. Understands "Cardiology" from the ontology
2. Queries Lakehouse for patient assignments
3. Queries Eventhouse for live heart rates
4. Combines the results
5. Returns the answer

No SQL or KQL is required.

---

## Improving Accuracy

### Data Agent Instructions

Provide guidance such as:

- Which source to use
- Preferred terminology
- Business rules

---

### Example Queries

Supply sample question-and-answer pairs.

Example:

Question:

> Show ICU occupancy.

Expected query:

```
Retrieve all occupied ICU rooms
```

These examples help the AI generate better responses.

---

## Security

Data Agents:

- Enforce read-only access
- Respect user permissions
- Apply Fabric security automatically

---

## Integration

Data Agents can be published to:

- Microsoft 365 Copilot
- Microsoft Copilot Studio

---

# 3. Graph in Microsoft Fabric

## Purpose

Graph provides native graph storage and graph computation for connected data.

Instead of joining relational tables repeatedly, Graph stores relationships directly.

---

## Graph Model

Graph consists of:

### Nodes

Represent entities.

Examples:

- Hospital
- Department
- Room
- Patient

---

### Edges

Represent relationships.

Examples:

- Contains
- Assigned To
- Occupies
- Belongs To

---

## Example Graph

```text
Hospital
    │
contains
    ▼
Department
    │
contains
    ▼
Room
    │
occupied by
    ▼
Patient
```

---

## Query Language

Graph uses:

**GQL (Graph Query Language)**

An international standard for graph databases.

---

## Example Questions

- Which patients occupy surgical rooms?
- Which departments belong to Hospital A?
- Show patient movement across rooms.
- Show department hierarchy.

---

## Healthcare Example

Graph traversal:

```
Hospital
      ↓
Departments
      ↓
Rooms
      ↓
Patients
```

Relationships are traversed directly without complex joins.

---

## Advantages

- Native graph database
- No ETL required
- Uses OneLake directly
- Visual relationship exploration
- Large-scale graph support

---

# Ontology + Graph Integration

The ontology defines:

- Entities
- Properties
- Relationships

Graph automatically creates the underlying graph structure.

```text
Ontology
      │
Automatically Creates
      ▼
Graph Database
      │
      ▼
Visualization
Traversal
Relationship Queries
```

---

# 4. Semantic Models

## Purpose

Power BI Semantic Models provide an excellent starting point for building ontologies.

Instead of creating everything manually, Fabric IQ can generate ontology components automatically.

---

## Automatically Generated

Fabric IQ creates:

- Entity Types
- Properties
- Relationships
- Keys

based on the semantic model.

---

## Example

Semantic Model Tables

```
Hospital
Department
Room
Patient
```

becomes

```
Entity Types

Hospital
Department
Room
Patient
```

Columns become:

```
Properties
```

Relationships become:

```
Relationship Types
```

Primary Keys become:

```
Entity Keys
```

---

## Benefits

Instead of manually creating every concept:

- Generate ontology automatically
- Save development time
- Preserve existing modeling work

---

## After Generation

Refine the ontology by:

- Verifying entity keys
- Checking bindings
- Adding Eventhouse entities
- Enhancing relationships
- Connecting additional data sources

---

## Example Enhancement

Initial ontology:

```
Hospital
Department
Room
Patient
```

Later extended with:

```
VitalSign
MedicalDevice
Sensor
```

from Eventhouse.

---

# End-to-End Workflow

```text
Power BI Semantic Model
            │
Generate Ontology
            │
            ▼
Ontology Item
(Entity Types, Properties, Relationships)
            │
            ▼
Bind OneLake Data
(Lakehouse + Eventhouse)
            │
            ▼
Managed Graph
            │
            ├─────────────┐
            ▼             ▼
      Graph Queries   Data Agents
       (GQL)         (Natural Language)
```

---

# Component Comparison

| Component | Purpose | Output |
|-----------|---------|--------|
| Ontology Item | Define business vocabulary | Business concepts |
| Data Agent | Natural language Q&A | AI-generated answers |
| Graph | Relationship traversal and visualization | Connected data exploration |
| Semantic Model | Generate ontology foundation | Prebuilt ontology structure |

---

# Key Benefits of Fabric IQ Components

- Shared business vocabulary
- AI-powered natural language querying
- Automatic ontology generation
- Native graph database
- Cross-source federated queries
- No data duplication
- OneLake integration
- Secure access control
- Visual relationship exploration
- Seamless integration across Microsoft Fabric
