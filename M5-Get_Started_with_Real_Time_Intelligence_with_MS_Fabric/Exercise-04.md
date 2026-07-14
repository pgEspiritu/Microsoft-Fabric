# ⚡ Get Started with Real-Time Intelligence in Microsoft Fabric

## 📖 Overview

**Microsoft Fabric Real-Time Intelligence** enables organizations to ingest, process, analyze, and visualize streaming data in real time.

Using Real-Time Intelligence, you can:

- Stream data from various sources
- Store streaming data in an **Eventhouse**
- Query data using **Kusto Query Language (KQL)**
- Build live dashboards
- Create alerts using **Activator**

In this lab, you'll build a complete real-time analytics solution using **sample stock market data**.

---

## 🎯 Objectives

In this lab, you will learn how to:

- Create a Microsoft Fabric workspace
- Create an Eventstream
- Stream sample stock market data
- Create an Eventhouse
- Store streaming data in a KQL database
- Query streaming data with KQL
- Build a Real-Time Dashboard
- Create alerts using Activator
- Clean up Fabric resources

---

## ⏱ Estimated Time

**30 minutes**

---

## 📋 Prerequisites

- Microsoft Fabric account
- Microsoft Fabric tenant
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
RealTimeLab
```

5. Under **Advanced**, choose a licensing mode that includes Fabric capacity:

- Fabric Trial
- Fabric
- Power BI Premium

6. Open the workspace.

The workspace should initially be empty.

---

# Part 2 — Create an Eventstream

Open:

```text
Real-Time Hub
```

> **Note**
>
> If **Real-Time Hub** is not visible:
>
> ```text
> ...
> → Pin Real-Time Hub
> ```

Select:

```text
Add Data
```

Choose:

```text
Stock Market Sample Data
```

Configure the source:

| Setting | Value |
|----------|-------|
| Source Name | stock |
| Workspace | Your workspace |
| Eventstream Name | stock-data |

The default stream will be created as:

```text
stock-data-stream
```

Click:

```text
Next
```

Then:

```text
Connect
```

Select:

```text
Open Eventstream
```

The Eventstream canvas should display:

- Stock Source
- stock-data-stream

---

# Part 3 — Create an Eventhouse

Select:

```text
Create
```

Under:

```text
Real-Time Intelligence
```

Choose:

```text
Eventhouse
```

Provide a unique name.

Example:

```text
StockEventhouse
```

Wait until the Eventhouse opens.

---

## Explore the Eventhouse

Notice that the Eventhouse automatically includes:

- KQL Database
- Queryset

Initially, no tables exist.

---

# Part 4 — Load Streaming Data into an Eventhouse

Inside the Eventhouse:

Select:

```text
Get Data
```

Choose:

```text
Eventstream
→ Existing Eventstream
```

Create a new destination table.

Table name:

```text
stock
```

Configure:

| Setting | Value |
|----------|-------|
| Workspace | Your workspace |
| Eventstream | stock-data |
| Connection Name | stock-table |

Continue through the remaining wizard.

Inspect the data.

Finish the setup.

The Eventhouse now contains:

```text
stock
```

table.

---

# Part 5 — Verify the Eventstream

Open:

```text
Real-Time Hub
```

Locate:

```text
stock-data-stream
```

Select:

```text
...
→ Open Eventstream
```

The Eventstream should now display:

- Source
- Destination (stock table)

If no preview appears:

```text
Refresh
```

> **Note**
>
> In production solutions, Eventstreams often include transformations such as:
>
> - Filtering
> - Aggregation
> - Windowing
> - Data enrichment

---

# Part 6 — Query Streaming Data

Open your:

```text
Eventhouse Database
```

Select:

```text
Queryset
```

Replace the first sample query with:

```kusto
stock
| take 100
```

Run the query.

The first 100 streaming events are displayed.

---

## Calculate Average Price

Replace the query with:

```kusto
stock
| where ["time"] > ago(5m)
| summarize avgPrice = avg(todecimal(bidPrice)) by symbol
| project symbol, avgPrice
```

Run the query.

Wait a few seconds.

Run it again.

Notice that the average prices continuously update as new streaming events arrive.

---

# Part 7 — Create a Real-Time Dashboard

Highlight the previous KQL query.

Select:

```text
Save to Dashboard
```

Create a new dashboard.

Settings:

| Setting | Value |
|----------|-------|
| Dashboard Name | Stock Dashboard |
| Tile Name | Average Prices |

Create and open the dashboard.

Initially, the visualization appears as a table.

---

## Change the Visualization

Switch:

```text
Viewing Mode
```

to

```text
Editing Mode
```

Edit the tile.

Under:

```text
Visual Formatting
```

Change:

```text
Table
```

to

```text
Column Chart
```

Apply the changes.

The dashboard now displays a live chart of average stock prices.

---

# Part 8 — Create an Alert

Inside the dashboard:

Select:

```text
Set Alert
```

Configure:

| Setting | Value |
|----------|-------|
| Run Query Every | 5 minutes |
| Check | On each event grouped by |
| Grouping Field | symbol |
| When | avgPrice |
| Condition | Increases by |
| Value | 100 |
| Action | Send me an email |

Save Location:

| Setting | Value |
|----------|-------|
| Workspace | Your workspace |
| Item | Create new item |
| Name | Any unique name |

Create the alert.

Close the confirmation window.

---

# Part 9 — View the Activator

Return to your workspace.

You should now see several items:

- Eventstream
- Eventhouse
- KQL Database
- Dashboard
- Activator

Open:

```text
Activator
```

Expand:

```text
avgPrice
```

Select your alert.

Open:

```text
History
```

If the stock price has not yet increased by more than **100**, no alert history will appear.

Whenever the condition is met:

- An email notification is sent.
- The event is recorded in the History page.

---

# Part 10 — Clean Up Resources

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

- Create a Microsoft Fabric workspace
- Build an Eventstream
- Stream real-time stock market data
- Create an Eventhouse
- Store streaming events in a KQL database
- Query streaming data using Kusto Query Language (KQL)
- Build a Real-Time Dashboard
- Visualize live streaming data
- Configure alerts with Activator
- Clean up Microsoft Fabric resources
