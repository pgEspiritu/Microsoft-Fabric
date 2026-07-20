# Design Scalable Semantic Models

In this exercise, you will work with DAX functions to enhance the flexibility and efficiency of semantic models by using **calculation groups** and **field parameters**. These features enable highly interactive reports without creating multiple visuals or writing complex DAX expressions.

## Objectives

By completing this lab, you will learn how to:

- Use DAX functions to modify relationship behavior.
- Create calculation groups and apply dynamic time intelligence calculations.
- Create field parameters to dynamically switch fields and measures.

**Estimated time:** 30 minutes

---

# Before You Start

> **Prerequisites**
>
> - Power BI Desktop **November 2025** or later.

## Download Lab Files

Download the starter file:

- https://github.com/MicrosoftLearning/mslearn-fabric/raw/main/Allfiles/Labs/15/15-scalable-semantic-models.zip

Extract the contents to:

```text
C:\Users\Student\Downloads\15-scalable-semantic-models
```

Open:

```text
15-Starter-Sales Analysis.pbix
```

> **Note**
>
> If prompted to apply changes, ignore the warning and close it.
> Do **not** select **Discard changes**.

---

# Work with Relationships

In this task, you'll examine the existing data model and understand active and inactive relationships.

## Open Model View

1. Open **Power BI Desktop**.
2. Select **Model view**.

The model contains:

- **Date** table
- **Sales** table

Notice three relationships between the two tables.

### Observe the Relationships

Hover over each relationship.

Notice:

- `Date[Date]` → `Sales[OrderDate]` (**Active**)
- `Date[Date]` → `Sales[ShipDate]` (**Inactive**)
- `Date[Date]` → `Sales[DueDate]` (**Inactive**)

The **Date** table acts as a **role-playing dimension**, allowing multiple date meanings:

- Order Date
- Ship Date
- Due Date

Only one relationship can be active at a time.

---

# Visualize Sales by Date

## Create a Table Visual

Switch to **Report view**.

Insert a **Table** visual.

Add:

- `Date[Year]`
- `Sales[Total Sales]`

The table displays:

| Year | Total Sales |
|------|-------------|

Because the active relationship uses **OrderDate**, sales are grouped by **Order Year**.

---

# Use Inactive Relationships

Instead of creating duplicate Date tables, use the **USERELATIONSHIP()** function.

## Create a Measure

Right-click the **Sales** table.

Select:

```
New measure
```

Enter:

```DAX
Sales Shipped =
CALCULATE (
    SUM('Sales'[Sales]),
    USERELATIONSHIP('Date'[Date], 'Sales'[ShipDate])
)
```

### Explanation

- `CALCULATE()` changes filter context.
- `USERELATIONSHIP()` temporarily activates the ShipDate relationship.

Add **Sales Shipped** to the table.

Observe:

- Grand total remains identical.
- Yearly values differ because shipments can occur after orders.

---

# Create Calculation Groups

Calculation groups eliminate the need to create many repetitive measures.

## Create a Calculation Group

Switch to **Model view**.

Select:

```
Calculation Group
```

If prompted, choose **Yes**.

Rename:

| Object | Name |
|---------|------|
| Calculation Group | Time Calculations |
| Calculation Column | Yearly Calculations |

> **Note**
>
> After creating a calculation group, Power BI no longer creates implicit measures automatically.

---

## Create Calculation Item: Year-to-Date

Select the automatically created calculation item.

Replace the formula with:

```DAX
Year-to-Date (YTD) =
CALCULATE(
    SELECTEDMEASURE(),
    DATESYTD('Date'[Date])
)
```

---

## Create Calculation Item: Previous Year

Right-click **Calculation items**

Select:

```
New calculation item
```

Enter:

```DAX
Previous Year (PY) =
CALCULATE(
    SELECTEDMEASURE(),
    PREVIOUSYEAR('Date'[Date])
)
```

---

## Create Calculation Item: Year-over-Year Growth

Create another calculation item:

```DAX
Year-over-Year (YoY) Growth =
VAR MeasurePriorYear =
    CALCULATE(
        SELECTEDMEASURE(),
        SAMEPERIODLASTYEAR('Date'[Date])
    )
RETURN
DIVIDE(
    (SELECTEDMEASURE() - MeasurePriorYear),
    MeasurePriorYear
)
```

---

## Add Dynamic Formatting

Select the **YoY** calculation item.

Enable:

```
Dynamic format string
```

Set the **Format** expression:

```DAX
"0.##%"
```

Your calculation group should contain:

- Year-to-Date (YTD)
- Previous Year (PY)
- Year-over-Year (YoY) Growth

---

# Apply Calculation Groups

Switch back to **Report view**.

Open the **Overview** page.

Select the existing **Matrix** visual.

Drag:

```
Yearly Calculations
```

to the **Columns** field.

The matrix now displays:

- Current values
- Previous Year
- Year-to-Date
- YoY Growth

for each measure.

---

# Create Field Parameters

Field parameters allow users to dynamically switch measures.

## Create a Parameter

Go to:

```
Modeling
→ New parameter
→ Fields
```

Configure:

**Name**

```
Sales Figures
```

Enable:

```
✓ Add slicer to this page
```

Add these measures:

- Total Sales
- Profit
- Profit Margin
- Orders

Select:

```
Create
```

---

## Use the Field Parameter

Select the Matrix.

Remove existing fields from:

```
Values
```

Replace with:

```
Sales Figures
```

Use the slicer to switch between:

- Total Sales
- Profit
- Profit Margin
- Orders

The matrix automatically updates.

---

# Edit the Field Parameter

Open the **Salesperson Performance** page.

The existing report uses bookmark buttons to switch measures.

Replace this approach with the field parameter.

## Replace the X-Axis

Select the clustered bar chart.

Replace:

```
Total Sales
```

with:

```
Sales Figures
```

---

## Add a Slicer

Insert a **Slicer** visual.

Add:

```
Sales Figures
```

---

## Add Target to the Parameter

Select the **Sales Figures** parameter.

Replace its DAX definition with:

```DAX
Sales Figures = {
    ("Total Sales", NAMEOF('Sales'[Total Sales]), 0),
    ("Profit", NAMEOF('Sales'[Profit]), 1),
    ("Profit Margin", NAMEOF('Sales'[Profit Margin]), 2),
    ("Orders", NAMEOF('Sales'[Orders]), 3),
    ("Target", NAMEOF('Targets'[Target]), 4)
}
```

Commit the changes.

The slicer now switches between:

- Total Sales
- Profit
- Profit Margin
- Orders
- Target

---

# Remove Bookmark Buttons

Delete the old bookmark buttons from the report.

The report now relies entirely on the field parameter for measure selection, making it more scalable and easier to maintain.

---

# Lab Complete

In this exercise, you learned how to:

- Work with active and inactive relationships.
- Use `USERELATIONSHIP()` inside measures.
- Create reusable calculation groups.
- Implement dynamic time intelligence.
- Create and edit field parameters.
- Build flexible, scalable semantic models.

Close **Power BI Desktop**.

No need to save the report.
