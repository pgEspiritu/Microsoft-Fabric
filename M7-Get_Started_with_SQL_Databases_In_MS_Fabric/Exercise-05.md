# 🗄️ Work with SQL Database in Microsoft Fabric

## 📖 Overview

**SQL Database in Microsoft Fabric** is a developer-friendly transactional database built on the same SQL Database engine that powers **Azure SQL Database**.

It enables you to:

- Create operational databases
- Run T-SQL queries
- Insert, update, and delete data
- Integrate external datasets
- Secure data with views and roles
- Build applications directly within Microsoft Fabric

---

## 🎯 Objectives

In this lab, you will learn how to:

- Create a Microsoft Fabric workspace
- Create a SQL Database
- Load sample data
- Query relational data using T-SQL
- Integrate external data
- Create views
- Secure data with SQL roles
- Clean up Fabric resources

---

## ⏱ Estimated Time

**30 minutes**

---

## 📋 Prerequisites

- Microsoft Fabric account
- Fabric Trial, Premium, or Paid Capacity

---

# Part 1 — Create a Workspace

1. Open Microsoft Fabric:

   https://app.fabric.microsoft.com/home?experience=fabric

2. Sign in.

3. Select:

```text
New Workspace
```

4. Create a workspace.

Example:

```text
SQLDatabaseLab
```

5. Under **Advanced**, choose:

- Fabric Trial
- Fabric
- Power BI Premium

6. Open the workspace.

The workspace should initially be empty.

---

# Part 2 — Create a SQL Database

Select:

```text
Create
```

Under:

```text
Databases
```

Choose:

```text
SQL Database
```

Database name:

```text
AdventureWorksLT
```

Click:

```text
Create
```

After the database is created:

Select:

```text
Sample Data
```

Load the sample dataset.

Wait until the sample data has finished loading.

---

# Part 3 — Query the SQL Database

Open:

```text
Home
→ New Query
```

Run:

```sql
SELECT
    p.Name AS ProductName,
    pc.Name AS CategoryName,
    p.ListPrice
FROM SalesLT.Product p
INNER JOIN SalesLT.ProductCategory pc
    ON p.ProductCategoryID = pc.ProductCategoryID
ORDER BY p.ListPrice DESC;
```

This query returns:

- Product name
- Category
- List price

sorted by price (highest first).

---

## Query Customer Orders

Create another SQL query.

Run:

```sql
SELECT
    c.FirstName,
    c.LastName,
    soh.OrderDate,
    soh.SubTotal
FROM SalesLT.Customer c
INNER JOIN SalesLT.SalesOrderHeader soh
    ON c.CustomerID = soh.CustomerID
ORDER BY soh.OrderDate DESC;
```

This query displays:

- Customer name
- Order date
- Order subtotal

sorted by newest orders.

Close all query tabs.

---

# Part 4 — Integrate External Data

## Create a Public Holidays Table

Create a new SQL query.

Run:

```sql
CREATE TABLE SalesLT.PublicHolidays
(
    CountryOrRegion NVARCHAR(50),
    HolidayName NVARCHAR(100),
    Date DATE,
    IsPaidTimeOff BIT
);
```

---

## Insert Holiday Records

Run:

```sql
INSERT INTO SalesLT.PublicHolidays
(
    CountryOrRegion,
    HolidayName,
    Date,
    IsPaidTimeOff
)
VALUES
('Canada','Victoria Day','2024-02-19',1),
('United Kingdom','Christmas Day','2024-12-25',1),
('United Kingdom','Spring Bank Holiday','2024-05-27',1),
('United States','Thanksgiving Day','2024-11-28',1);
```

The table now contains public holiday information for:

- Canada
- United Kingdom
- United States

---

## Insert Sample Addresses and Orders

Run:

```sql
-- Insert new addresses
INSERT INTO SalesLT.Address
(
    AddressLine1,
    City,
    StateProvince,
    CountryRegion,
    PostalCode,
    rowguid,
    ModifiedDate
)
VALUES
('123 Main St','Seattle','WA','United States','98101',NEWID(),GETDATE()),
('456 Maple Ave','Toronto','ON','Canada','M5H 2N2',NEWID(),GETDATE()),
('789 Oak St','London','England','United Kingdom','EC1A 1BB',NEWID(),GETDATE());

-- Insert sample orders
INSERT INTO SalesLT.SalesOrderHeader
(
    SalesOrderID,
    RevisionNumber,
    OrderDate,
    DueDate,
    ShipDate,
    Status,
    OnlineOrderFlag,
    PurchaseOrderNumber,
    AccountNumber,
    CustomerID,
    ShipToAddressID,
    BillToAddressID,
    ShipMethod,
    CreditCardApprovalCode,
    SubTotal,
    TaxAmt,
    Freight,
    Comment,
    rowguid,
    ModifiedDate
)
VALUES
(
1001,1,'2024-12-25','2024-12-30','2024-12-26',1,1,
'PO12345','AN123',1,
(SELECT TOP 1 AddressID FROM SalesLT.Address WHERE AddressLine1='789 Oak St'),
(SELECT TOP 1 AddressID FROM SalesLT.Address WHERE AddressLine1='123 Main St'),
'Ground','12345',
100.00,10.00,5.00,'New Order 1',
NEWID(),GETDATE()
),

(
1002,1,'2024-11-28','2024-12-03','2024-11-29',1,1,
'PO67890','AN456',2,
(SELECT TOP 1 AddressID FROM SalesLT.Address WHERE AddressLine1='123 Main St'),
(SELECT TOP 1 AddressID FROM SalesLT.Address WHERE AddressLine1='456 Maple Ave'),
'Air','67890',
200.00,20.00,10.00,'New Order 2',
NEWID(),GETDATE()
),

(
1003,1,'2024-02-19','2024-02-24','2024-02-20',1,1,
'PO54321','AN789',3,
(SELECT TOP 1 AddressID FROM SalesLT.Address WHERE AddressLine1='456 Maple Ave'),
(SELECT TOP 1 AddressID FROM SalesLT.Address WHERE AddressLine1='789 Oak St'),
'Sea','54321',
300.00,30.00,15.00,'New Order 3',
NEWID(),GETDATE()
),

(
1004,1,'2024-05-27','2024-06-01','2024-05-28',1,1,
'PO98765','AN321',4,
(SELECT TOP 1 AddressID FROM SalesLT.Address WHERE AddressLine1='789 Oak St'),
(SELECT TOP 1 AddressID FROM SalesLT.Address WHERE AddressLine1='789 Oak St'),
'Ground','98765',
400.00,40.00,20.00,'New Order 4',
NEWID(),GETDATE()
);
```

This inserts fictional addresses and sales orders for multiple countries.

---

## Match Sales Orders with Public Holidays

Run:

```sql
SELECT DISTINCT
    soh.SalesOrderID,
    soh.OrderDate,
    ph.HolidayName,
    ph.CountryOrRegion
FROM SalesLT.SalesOrderHeader AS soh
INNER JOIN SalesLT.Address a
    ON a.AddressID = soh.ShipToAddressID
INNER JOIN SalesLT.PublicHolidays AS ph
    ON soh.OrderDate = ph.Date
   AND a.CountryRegion = ph.CountryOrRegion;
```

This query identifies orders placed on public holidays.

---

# Part 5 — Secure the Data

## Create a Filtered View

Run:

```sql
CREATE VIEW SalesLT.vw_SalesOrderHoliday
AS
SELECT DISTINCT
    soh.SalesOrderID,
    soh.OrderDate,
    ph.HolidayName,
    ph.CountryOrRegion
FROM SalesLT.SalesOrderHeader AS soh
INNER JOIN SalesLT.Address a
    ON a.AddressID = soh.ShipToAddressID
INNER JOIN SalesLT.PublicHolidays AS ph
    ON soh.OrderDate = ph.Date
   AND a.CountryRegion = ph.CountryOrRegion
WHERE a.CountryRegion = 'United Kingdom';
```

The view exposes only orders shipped to the **United Kingdom**.

---

## Create a Database Role

Run:

```sql
CREATE ROLE SalesOrderRole;
```

Grant permissions:

```sql
GRANT SELECT
ON SalesLT.vw_SalesOrderHoliday
TO SalesOrderRole;
```

Users assigned to **SalesOrderRole** can query only the filtered view.

Attempting to access unauthorized objects produces an error similar to:

```text
Msg 229, Level 14, State 5

The SELECT permission was denied
on the object 'ObjectName',
database 'DatabaseName',
schema 'SchemaName'.
```

---

# Part 6 — Clean Up Resources

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

- Create a Microsoft Fabric SQL Database
- Load sample data
- Query relational tables using T-SQL
- Join multiple tables
- Create new database tables
- Integrate external data
- Analyze sales orders against public holidays
- Secure data using SQL views and roles
- Clean up Microsoft Fabric resources
