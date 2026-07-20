# Introduction

Imagine you're a data analyst at **Lamna Healthcare**, responsible for helping clinical operations teams understand patient care patterns across your facility.

Patient records are stored in **Lakehouse** tables, while vital signs stream continuously from ICU monitoring equipment into an **Eventhouse**. When hospital administrators ask questions like:

- *Which patients in the ICU have elevated vital signs?*
- *How many beds are occupied on the surgical floor?*

you must manually:

- Join Lakehouse tables with Eventhouse streams.
- Translate business terms into technical column names.
- Write complex SQL or KQL queries.

Business users cannot explore the data themselves—they rely on you to write queries whenever they have questions. By the time answers are delivered, clinical conditions may already have changed.

**Fabric IQ** addresses this challenge by allowing you to define a shared business vocabulary through an **Ontology**, then bind those concepts to data stored in **OneLake**.

You define business concepts such as:

- Patient
- Department
- Room

along with their:

- Properties
- Relationships

creating a semantic layer over your data.

Business users can then:

- Ask questions in natural language using **Data Agents**.
- Visually explore relationships using **Graph in Microsoft Fabric**.

This enables users to explore data independently without requiring analysts to write queries for every request.

---

## In this module

You'll learn:

- What **Fabric IQ** is and how it works.
- The major Fabric IQ components:
  - Ontology
  - Data Agents
  - Graph in Microsoft Fabric
  - Power BI Semantic Models
- When to use each component.
- How ontology modeling shifts data design from **use-case-driven** thinking to **concept-driven** thinking.
- How Fabric IQ improves collaboration between business users and technical teams.
