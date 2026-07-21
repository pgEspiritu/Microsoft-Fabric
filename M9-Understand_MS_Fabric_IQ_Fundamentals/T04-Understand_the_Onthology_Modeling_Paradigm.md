# Understand the Ontology Modeling Paradigm

## Overview

Ontology modeling in **Microsoft Fabric IQ** focuses on modeling **business concepts** independently of specific reports, dashboards, or analytical use cases.

Unlike traditional analytical modeling, ontology modeling captures the meaning of business entities first and connects them to data later.

---

# Traditional Data Modeling vs Ontology Modeling

## Traditional Analytical Modeling

Traditional analytical models are designed around reporting requirements.

Typical questions include:

- What reports do we need?
- Which dimensions are required?
- Which fact tables should be created?
- How should the star schema be designed?

The resulting model is optimized for analytics.

Example:

```
FactSales
    │
    ├── PatientDim
    ├── RoomDim
    └── DepartmentDim
```

---

## Ontology Modeling

Ontology modeling starts with business understanding.

Typical questions include:

- What are the core business concepts?
- How are they related?
- What information describes each concept?

Reports and analytics are built afterward.

---

# Shift in Thinking

| Traditional Modeling | Ontology Modeling |
|----------------------|------------------|
| Tables first | Business concepts first |
| Reports drive design | Business meaning drives design |
| Database-centric | Business-centric |
| SQL relationships | Named semantic relationships |
| Physical schema | Conceptual model |

---

# Example: Healthcare

## Traditional Model

```
PatientDim
RoomDim
DepartmentDim
FactAdmissions
```

Columns may use technical names:

```
pt_id
rm_num
dept_id
```

Different teams may create inconsistent definitions.

Example:

```
Patient
Customer
Resident
```

may all refer to the same concept.

---

## Ontology Model

Business concepts are defined once.

Entity Types:

- Patient
- Room
- Department
- Hospital

Properties:

- PatientName
- DateOfBirth
- RoomNumber
- DepartmentName

Relationships:

- Department has Room
- Room assigned to Patient

Everyone uses the same business vocabulary.

---

# Ontology Example

```text
Hospital
     │
contains
     ▼
Department
     │
has
     ▼
Room
     │
assigned_to
     ▼
Patient
```

Relationships are explicitly named.

Unlike SQL foreign keys, they can be traversed directly.

---

# Entity Types

## Definition

Entity Types are reusable business concept definitions.

They exist independently of physical tables.

Examples:

- Patient
- Doctor
- Room
- Department
- Hospital

---

## Entity Types Define

- Name
- Description
- Identifier
- Properties

Later, they are bound to data sources.

---

# Entity Type Example

```
Entity Type

Patient
```

Properties:

```
PatientID
PatientName
DateOfBirth
Gender
AdmissionDate
```

Identifier:

```
PatientID
```

No data is stored here.

It is purely a conceptual definition.

---

# Properties

## Purpose

Properties describe an entity.

Ontology properties standardize business terminology regardless of source column names.

---

## Traditional Database Columns

Different databases may contain:

```
temp
temperature
temp_reading
body_temp
```

All represent the same concept.

---

## Ontology Property

Define one standardized property:

```
Temperature
```

During binding:

| Source Column | Ontology Property |
|--------------|-------------------|
| temp | Temperature |
| body_temp | Temperature |
| temp_reading | Temperature |

Applications always use:

```
Temperature
```

---

# Example: VitalSign Entity

Properties:

- HeartRate
- OxygenSaturation
- RespiratoryRate
- Timestamp

Regardless of source column names.

---

# Identifier Properties

Certain properties uniquely identify an entity.

Example:

```
PatientID
```

Benefits:

- Unique identification
- Entity resolution
- Consistent joins across sources

---

# Relationships

## Definition

Relationships are explicit, named, directional connections between entity types.

Unlike SQL foreign keys, relationships are business concepts.

---

## Example Relationships

```
Department
      │
has
      ▼
Room
```

```
Room
      │
assigned_to
      ▼
Patient
```

```
Patient
      │
has
      ▼
VitalSign
```

---

# Advantages

Relationships can be:

- Visualized
- Traversed
- Queried directly
- Understood by AI

No complex JOIN statements are required.

---

# Graph Traversal Example

Find all patients in a department.

Traversal:

```text
Department
      │
has
      ▼
Room
      │
assigned_to
      ▼
Patient
```

Instead of writing multiple SQL joins.

---

# Data Binding

## Purpose

Data Binding connects ontology concepts to actual data sources.

The ontology stores **metadata**, not the data itself.

---

## Supported Sources

- Lakehouse
- Eventhouse

---

## Example

Patient entity

↓

Lakehouse table

VitalSign entity

↓

Eventhouse stream

Each entity binds independently.

---

# No Data Duplication

Fabric IQ does **not** move or copy data.

Instead:

```text
Ontology
       │
References
       ▼
OneLake
```

Benefits:

- Single source of truth
- Reduced storage
- No ETL duplication

---

# Federated Queries

Since entities can bind to different systems:

```
Patient
    │
Lakehouse
```

```
VitalSign
    │
Eventhouse
```

Fabric IQ automatically performs federated queries.

Users see one integrated result.

---

# Data Binding Example

Source Table

| Source Column |
|--------------|
| HeartRate |
| OxygenSat |
| RespRate |

↓

Ontology Mapping

| Ontology Property |
|-------------------|
| HeartRate |
| OxygenSaturation |
| RespiratoryRate |

Business users always use standardized names.

---

# Benefits of Ontology Modeling

- Business-first design
- Shared business vocabulary
- Consistent definitions
- Reusable entity types
- Named relationships
- Standardized properties
- Cross-source integration
- AI-friendly semantic layer
- Graph-based exploration
- No data duplication

---

# Traditional vs Ontology Modeling

| Feature | Traditional Modeling | Ontology Modeling |
|---------|----------------------|------------------|
| Primary focus | Reports | Business concepts |
| Main objects | Tables | Entity Types |
| Attributes | Columns | Properties |
| Relationships | Foreign Keys | Named Relationships |
| Data movement | Often requires ETL | No duplication |
| Query style | SQL | Business concepts, Graph, AI |
| AI readiness | Limited | High |
| Cross-source support | Complex | Native via federated queries |

---

# Ontology Modeling Workflow

```text
Define Business Concepts
(Entity Types)
           │
           ▼
Define Properties
(Standard Business Names)
           │
           ▼
Define Relationships
(Business Connections)
           │
           ▼
Bind to Data Sources
(Lakehouse & Eventhouse)
           │
           ▼
Business Queries
 ├── Graph
 ├── AI Data Agents
 └── Query Builder
```

---

# Key Takeaways

- Ontology modeling starts with **business concepts**, not tables.
- Entity Types define reusable business objects.
- Properties standardize business terminology.
- Relationships are explicit and semantically meaningful.
- Data binding connects concepts to existing OneLake data without copying it.
- Fabric IQ enables federated queries across Lakehouse and Eventhouse.
- The resulting semantic layer supports Graph, AI agents, and natural language querying.
