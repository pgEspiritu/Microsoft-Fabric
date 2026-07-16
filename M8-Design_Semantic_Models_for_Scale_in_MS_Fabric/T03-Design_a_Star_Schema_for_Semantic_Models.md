# Design star schema for semantic models

You chose how data flows into your semantic model. Now design the star schema that organizes it for clear, performant queries. A star schema connects fact tables to dimension tables through relationships, creating the filter paths that reports and AI consumption depend on. If you're familiar with building star schema in Power BI Desktop, this unit focuses on the relationship design decisions that matter as models grow in complexity and scale.

## Star schema in a semantic model

In a star schema:

- **Fact tables** store measurable business events (such as sales transactions, order lines, and web visits).
- **Dimension tables** provide descriptive context (such as product details, customer information, and date attributes).

Dimension tables filter fact tables through relationships, allowing users to slice metrics by descriptive attributes.

> **Example:** A semantic model contains a central **FactSales** table connected to multiple dimensions such as **DimCustomer**, **DimProduct**, and **DimDate**, forming a star-shaped design.

In a Fabric semantic model, this structure provides clean filter propagation for both reports and AI experiences.

When Copilot or a Fabric data agent generates natural language queries, a well-designed star schema provides clear navigation paths to the correct data. Ambiguous or circular relationships make queries harder for both users and AI.

---

# How storage mode affects relationships

Relationship behavior depends on the semantic model's storage mode.

## Direct Lake relationships

In **Direct Lake**, relationships are read directly from Delta table metadata.

Relationships perform best when:

- Dimension key columns have low cardinality compared to fact table rows.
- Referential integrity is maintained.
- Relationship columns are indexed in the Delta tables.

When referential integrity exists, the engine can use **INNER JOIN** instead of **LEFT OUTER JOIN**, improving query performance.

> **Note:** If a query exceeds memory limits or uses unsupported operations, Direct Lake automatically falls back to DirectQuery, changing relationship behavior accordingly.

---

## Cross-source relationships

Fabric semantic models support relationships across multiple data stores.

Examples include:

- Lakehouse fact tables joined to Warehouse dimension tables.
- Warehouse tables joined to SQL analytics endpoint tables.

These scenarios use **Composite Models**.

At query time:

- Each source is queried independently.
- Fabric combines the results through the defined relationship.

---

# Relationship types

## One-to-many relationships

This is the standard relationship in a star schema.

Characteristics:

- One unique value in the dimension table.
- Multiple matching rows in the fact table.

Example:

```
DimProduct (1)
        |
        |
        |
FactSales (*)
```

Configure:

- Filter direction:
  - **Dimension → Fact**
- Cardinality:
  - **One-to-Many**

This is the recommended configuration for nearly all star schemas.

---

## Many-to-many relationships

Use when neither table contains unique values.

Instead of connecting them directly, create a **Bridge Table**.

Example:

```
Customer
     |
CustomerAccountBridge
     |
Account
```

The bridge table contains unique combinations of keys.

This converts the design into two One-to-Many relationships.

---

# Filter direction

### Recommended

Single-direction filtering:

```
Dimension
     ↓
Fact
```

Benefits:

- Predictable filtering
- Better performance
- Simpler DAX
- Fewer ambiguous query paths

---

### Use bi-directional filtering only when necessary

Typical scenarios:

- Many-to-many relationships
- Fact table filtering dimension tables

Downsides:

- Slower queries
- Ambiguous filter propagation
- Harder troubleshooting

Use sparingly.

---

# Referential integrity

The **Assume referential integrity** setting tells Fabric to use **INNER JOIN** rather than **LEFT OUTER JOIN**.

Advantages:

- Faster joins
- Fewer rows processed
- Better Direct Lake and DirectQuery performance

Enable only if:

Every foreign key in the fact table has a matching primary key in the dimension.

Otherwise:

Rows without matching dimension values are silently excluded from results.

---

# Inactive relationships and USERELATIONSHIP

Only one relationship between two tables can be active.

Example:

Sales table contains:

- OrderDate
- ShipDate

Both connect to:

```
DimDate
```

Only one can be active.

The second relationship remains inactive until needed.

Use the DAX `USERELATIONSHIP` function.

```DAX
Shipped Amount =
CALCULATE(
    SUM(Sales[Amount]),
    USERELATIONSHIP(Sales[ShipDate], 'Date'[Date])
)
```

This activates the ShipDate relationship only during calculation.

Benefits:

- Clean model
- Multiple analytical perspectives
- No duplicate date tables

---

# Handle snowflake schema in semantic models

Source systems often use normalized snowflake schemas.

Example:

```
Category
    |
Subcategory
    |
Product
    |
FactSales
```

In Fabric semantic models, you have two options.

---

## Option 1: Flatten into a star schema (Recommended)

Combine:

- Product
- Subcategory
- Category

into one dimension:

```
DimProduct
```

Advantages:

- Fewer tables
- Fewer joins
- Simpler DAX
- Faster queries
- Better AI understanding
- Easier maintenance

Flatten during:

- SQL transformations
- Power Query
- Dataflows
- Notebooks

before loading into the semantic model.

---

## Option 2: Preserve the snowflake

Keep the normalized hierarchy when:

- Dimensions contain many hierarchy levels.
- Multiple fact tables share the same subdimensions.
- Row-Level Security must be applied at intermediate levels.

Relationship example:

```
Category
    ↓
Subcategory
    ↓
Product
    ↓
FactSales
```

Configure each relationship using **single-direction filtering** toward the fact table.

---

> **Recommendation:** Flatten dimensions whenever possible. Use snowflake structures only when there is a clear business or technical requirement.

---

# Composite models for cross-source scenarios

Composite models allow tables to use different storage modes within the same semantic model.

Common scenarios include:

- Lakehouse fact tables with Warehouse dimension tables
- Eventhouse streaming data with historical Lakehouse data
- Imported external reference tables with Direct Lake fact tables

Example:

| Table | Source | Storage Mode |
|--------|--------|--------------|
| FactSales | Lakehouse | Direct Lake |
| DimCustomer | Warehouse | Direct Lake |
| ExchangeRates | External SQL | Import |
| LiveOrders | Operational DB | DirectQuery |

When using composite models:

- Configure each table's storage mode independently.
- Test cross-source relationships.
- Validate performance at expected production scale.

---

# Key Takeaways

- Design semantic models using a **Star Schema** whenever possible.
- Fact tables store measures; dimension tables provide descriptive context.
- Use **One-to-Many** relationships with **single-direction filtering**.
- Maintain **referential integrity** for better Direct Lake performance.
- Use **Bridge Tables** for Many-to-Many relationships.
- Keep alternate relationships inactive and activate them using **USERELATIONSHIP()**.
- Flatten snowflake schemas unless normalization is required.
- Use **Composite Models** when combining Fabric and external data sources.
- Simple relationships improve report performance, DAX maintenance, and AI-powered experiences such as Copilot.
