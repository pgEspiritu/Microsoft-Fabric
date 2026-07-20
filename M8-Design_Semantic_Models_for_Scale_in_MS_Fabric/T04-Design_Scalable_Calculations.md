# Design scalable calculations

Your model is structured. Now design the calculations that keep it performant and maintainable as your data and team grow.

At a small scale, duplicated measures and inconsistent naming may still work. As your semantic model grows to hundreds of measures and many developers, poor design becomes difficult to maintain and slows query performance.

This unit focuses on three scalable design patterns:

- **Calculation Groups** to reduce measure proliferation.
- **Readable DAX** for maintainability.
- **Aggregations** for improving performance on large datasets.

---

# Calculation groups

Calculation groups are reusable model objects that apply the same calculation pattern across multiple measures.

Instead of creating separate measures for every variation, you define the calculation once and apply it dynamically.

---

## The problem calculation groups solve

Imagine a model containing **50 base measures**:

- Total Sales
- Total Cost
- Profit
- Units Sold
- etc.

Each measure requires:

- Year-to-Date (YTD)
- Quarter-to-Date (QTD)
- Month-to-Date (MTD)

Without calculation groups:

```
50 measures
× 3 time calculations
---------------------
150 additional measures
```

If you also add:

- Previous Year
- Year-over-Year %
- Running Total

you can easily exceed **250+ measures**.

Maintaining that many measures becomes difficult.

---

## How calculation groups work

A calculation group contains multiple **Calculation Items**.

Each calculation item modifies the currently selected measure using:

```DAX
SELECTEDMEASURE()
```

Example:

### Year-to-Date

```DAX
CALCULATE(
    SELECTEDMEASURE(),
    DATESYTD('Date'[Date])
)
```

---

### Quarter-to-Date

```DAX
CALCULATE(
    SELECTEDMEASURE(),
    DATESQTD('Date'[Date])
)
```

---

### Month-to-Date

```DAX
CALCULATE(
    SELECTEDMEASURE(),
    DATESMTD('Date'[Date])
)
```

Users simply choose:

```
Time Intelligence

○ Current
○ MTD
○ QTD
○ YTD
```

The same calculation automatically applies to:

- Total Sales
- Profit
- Cost
- Units Sold

No duplicate measures are required.

---

# Dynamic format strings

Calculation groups can also dynamically change how results are displayed.

Example:

A Year-over-Year percentage should display as:

```
15.6%
```

instead of

```
0.156
```

Example format string:

```DAX
"0.0%"
```

Benefits:

- No duplicate formatted measures
- Consistent formatting
- Easier maintenance

---

## When to use calculation groups

Use calculation groups when **three or more measures** require the same calculation pattern.

Common scenarios:

- Year-to-Date
- Quarter-to-Date
- Month-to-Date
- Previous Year
- Running Totals
- Currency Conversion
- Budget vs Actual
- Variance Analysis

---

# DAX readability discipline

As semantic models grow, readable DAX becomes essential.

Readable DAX:

- reduces bugs
- simplifies maintenance
- helps new developers understand the model
- improves long-term scalability

---

## Use variables

Variables store intermediate calculations.

Benefits:

- Better readability
- Improved performance
- Avoid repeated calculations

Example:

```DAX
Profit Margin =
VAR TotalRevenue = SUM(Sales[Revenue])
VAR TotalCost = SUM(Sales[Cost])
VAR ProfitAmount = TotalRevenue - TotalCost

RETURN
    DIVIDE(ProfitAmount, TotalRevenue)
```

Instead of repeatedly writing:

```DAX
SUM(Sales[Revenue])
```

the calculation is evaluated once and reused.

Benefits:

- Cleaner code
- Faster execution
- Easier debugging

---

# Naming conventions

Large semantic models often contain hundreds of measures.

Consistent naming helps everyone understand the model.

## Measures

Good:

```
Total Sales
Gross Profit
YoY Revenue Growth
Average Order Value
```

Avoid:

```
Measure1
Calc7_v2
Test
Temp
```

---

## Variables

Good:

```
TotalRevenue
ProfitAmount
AverageCost
CustomerCount
```

Avoid:

```
x
temp
abc
var1
```

---

## Calculation group items

Use names describing the business calculation.

Good:

```
Year-to-Date
Quarter-to-Date
Month-to-Date
Previous Year
```

Avoid technical names like:

```
DATESYTD Wrapper
Calc01
```

---

## AI benefits

Good measure names also improve AI.

Copilot understands:

```
YoY Revenue Growth
```

better than

```
Calc7_v2
```

Clear names and descriptions produce more accurate natural language responses.

---

# Iterator functions vs aggregation functions

Understanding the difference affects performance.

---

## Aggregation functions

Examples:

```DAX
SUM()
AVERAGE()
MAX()
MIN()
COUNT()
```

These summarize a single column.

Example:

```DAX
Total Sales =
SUM(Sales[Amount])
```

Advantages:

- Fast
- Uses optimized storage engine
- Recommended whenever possible

---

## Iterator functions

Examples:

```DAX
SUMX()
AVERAGEX()
MAXX()
MINX()
```

Iterators evaluate an expression for every row.

Example:

```DAX
Revenue =
SUMX(
    Sales,
    Sales[Quantity] * Sales[UnitPrice]
)
```

Each row is processed individually.

Use iterators only when row-level calculations are required.

Examples:

- Quantity × Unit Price
- Weighted Average
- Custom row calculations

---

## Performance comparison

| Aggregation Functions | Iterator Functions |
|----------------------|--------------------|
| SUM() | SUMX() |
| MAX() | MAXX() |
| MIN() | MINX() |
| AVERAGE() | AVERAGEX() |

Aggregation functions are generally faster because they summarize existing columns directly.

Iterators require row-by-row evaluation.

---

# Information functions for defensive DAX

Information functions make measures behave correctly under different filter contexts.

Common functions:

- `ISBLANK()`
- `HASONEVALUE()`
- `ISINSCOPE()`

Example:

```DAX
Sales per Customer =
IF(
    HASONEVALUE(Customer[CustomerID]),
    DIVIDE(
        SUM(Sales[Amount]),
        1
    ),
    DIVIDE(
        SUM(Sales[Amount]),
        DISTINCTCOUNT(Sales[CustomerID])
    )
)
```

Benefits:

- Prevents unexpected calculations
- Supports multiple report layouts
- Makes measures more reusable

---

# Aggregations

Aggregations improve performance on very large fact tables.

Instead of scanning millions of detailed rows, Fabric reads precomputed summary tables.

Example:

Detail table

```
FactSales
-------------------------
100 million rows
```

Aggregation table

```
Monthly Sales by Region
-----------------------
5,000 rows
```

When a report asks:

```
Monthly Sales by Region
```

Fabric retrieves data from the aggregation table instead of scanning the detail table.

Result:

- Faster visuals
- Faster DAX
- Lower compute cost

---

# When to use aggregations

Consider aggregations when:

- Fact tables contain millions of rows.
- Reports usually display summarized data.
- Users experience slow report performance.
- Most queries don't require transaction-level detail.

Common aggregation levels:

- Daily Sales
- Monthly Sales
- Sales by Region
- Sales by Product Category

---

# Aggregations by storage mode

## Import Mode

Aggregation tables are stored as hidden Import tables.

The engine automatically redirects compatible queries to these tables.

Benefits:

- Excellent performance
- Reduced scanning

---

## Direct Lake Mode

Direct Lake already reads highly optimized Delta Parquet files.

Many workloads perform well without aggregation tables.

Only create aggregations when monitoring shows repeated large summary queries that would benefit from precomputed results.

---

# Key Takeaways

- Use **Calculation Groups** to eliminate duplicate measures.
- Use **SELECTEDMEASURE()** to dynamically apply calculations.
- Use **Dynamic Format Strings** for consistent formatting.
- Write readable DAX using **variables** and descriptive naming conventions.
- Prefer aggregation functions (`SUM`) over iterator functions (`SUMX`) whenever possible.
- Use **Information Functions** (`HASONEVALUE`, `ISINSCOPE`, `ISBLANK`) to create robust, reusable measures.
- Create **Aggregations** for large fact tables to improve report performance.
- In **Direct Lake**, aggregations are optional and should only be added when workload patterns justify them.
