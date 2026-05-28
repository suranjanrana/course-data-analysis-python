# 📊 The Complete Power BI Course
### From Beginner to Advanced — Concepts, Contexts & DAX Formulas

---

> **Course Overview**
> This course is structured into five modules that take you from zero knowledge of Power BI to building advanced analytical solutions. Each module builds on the previous one. You will learn core concepts, data modeling principles, and an extensive library of DAX formulas — all with clear definitions, syntax, and real-world examples.

---

## 📋 Table of Contents

1. [Module 1 — Introduction to Power BI](#module-1--introduction-to-power-bi)
2. [Module 2 — Data Transformation with Power Query](#module-2--data-transformation-with-power-query)
3. [Module 3 — Data Modeling & Relationships](#module-3--data-modeling--relationships)
4. [Module 4 — DAX (Data Analysis Expressions)](#module-4--dax-data-analysis-expressions)
5. [Module 5 — Advanced DAX & Analytics](#module-5--advanced-dax--analytics)
6. [Module 6 — Visualizations & Publishing](#module-6--visualizations--publishing)
7. [Quick Reference — DAX Formula Cheat Sheet](#quick-reference--dax-formula-cheat-sheet)

---

# Module 1 — Introduction to Power BI

## 1.1 What Is Power BI?

Power BI is a business intelligence (BI) platform developed by Microsoft. It allows users to connect to data sources, transform and clean data, build data models, create interactive visualizations, and share reports and dashboards across an organization.

Power BI is used by data analysts, business analysts, and developers to turn raw data into meaningful insights.

### Power BI Components

| Component | Description |
|---|---|
| **Power BI Desktop** | Free Windows application for building reports and models |
| **Power BI Service** | Cloud-based platform (app.powerbi.com) for publishing and sharing |
| **Power BI Mobile** | iOS and Android apps for consuming reports on-the-go |
| **Power BI Gateway** | Bridge that connects on-premises data to the cloud service |
| **Power BI Report Builder** | Tool for creating paginated (pixel-perfect) reports |
| **Power BI Embedded** | API for embedding Power BI content in custom applications |

---

## 1.2 The Power BI Workflow

Understanding the standard workflow is essential before diving into technical details.

```
Step 1: Connect
    └── Connect to data sources (Excel, SQL, APIs, Cloud, etc.)

Step 2: Transform
    └── Clean and shape data using Power Query Editor

Step 3: Model
    └── Define relationships between tables, create hierarchies

Step 4: Analyze
    └── Write DAX measures and calculated columns

Step 5: Visualize
    └── Build charts, tables, maps, and dashboards

Step 6: Share
    └── Publish to Power BI Service, share with stakeholders
```

---

## 1.3 Data Sources

Power BI can connect to hundreds of data sources. The most common categories include:

- **Files**: Excel (.xlsx), CSV, JSON, XML, PDF
- **Databases**: SQL Server, MySQL, PostgreSQL, Oracle, Access
- **Cloud Services**: Azure, Snowflake, Google BigQuery, Amazon Redshift
- **Online Services**: SharePoint, Salesforce, Google Analytics, Dynamics 365
- **Web**: Scraping data from web pages via URL
- **Other**: ODBC, OData feeds, Python/R scripts

### Connectivity Modes

| Mode | Description | Use Case |
|---|---|---|
| **Import** | Data is copied into Power BI's in-memory engine | Best performance; data refreshes on a schedule |
| **DirectQuery** | Queries are sent live to the data source | Real-time data; no data stored in Power BI |
| **Live Connection** | Connects to a pre-built model (SSAS, Power BI Dataset) | Centralized enterprise models |
| **Composite** | Mixes Import and DirectQuery in one model | Flexibility for hybrid scenarios |

---

## 1.4 The Power BI Interface

### Power BI Desktop — Key Areas

```
┌────────────────────────────────────────────────────┐
│  RIBBON (File, Home, Insert, Modeling, View...)     │
├──────┬─────────────────────────────────┬────────────┤
│      │                                 │            │
│ VIEW │     CANVAS (Report Area)        │  FIELDS    │
│ PANE │                                 │  PANE      │
│      │   [Visuals appear here]         │            │
│  R   │                                 │  Tables    │
│  E   │                                 │  and       │
│  P   ├─────────────────────────────────┤  Columns   │
│  O   │  FILTERS PANE                   │  listed    │
│  R   │  (Page, Visual, Report level)   │  here      │
│  T   │                                 │            │
├──────┴─────────────────────────────────┴────────────┤
│  DATA VIEW   |  MODEL VIEW   |  REPORT VIEW          │
└────────────────────────────────────────────────────┘
```

### Three Main Views

- **Report View**: Where you build and design visualizations
- **Data View**: Where you inspect and explore table data, write calculated columns
- **Model View**: Where you define and manage relationships between tables

---

# Module 2 — Data Transformation with Power Query

## 2.1 What Is Power Query?

Power Query is the ETL (Extract, Transform, Load) engine built into Power BI. It allows you to connect to data, clean it, reshape it, and load it into the data model — all without writing code (though it uses a language called **M** behind the scenes).

Every transformation you apply is recorded as a step in the **Applied Steps** pane, making the process auditable and repeatable.

---

## 2.2 Core Transformation Operations

### 2.2.1 Remove Rows & Columns

- **Remove Columns**: Eliminate unnecessary fields
- **Remove Rows**: Remove top rows, blank rows, errors, or duplicates
- **Keep Top N Rows**: Retain only a specific number of rows

### 2.2.2 Data Type Conversion

Always set correct data types. Power BI handles:

| Data Type | Examples |
|---|---|
| Whole Number | 1, 100, -5 |
| Decimal Number | 3.14, 99.99 |
| Text | "Hello", "Product A" |
| Date | 2024-01-01 |
| Date/Time | 2024-01-01 09:30:00 |
| Boolean | TRUE / FALSE |
| Currency | $1,234.56 |

### 2.2.3 Split & Merge Columns

- **Split Column by Delimiter**: Split "First Last" into two columns using space as delimiter
- **Merge Columns**: Combine "City" and "Country" into one column

### 2.2.4 Pivot & Unpivot

- **Pivot**: Turns row values into column headers (wide format)
- **Unpivot**: Turns column headers into row values (long format — usually preferred for modeling)

**Example — Unpivoting:**

Before (wide):

| Product | Jan | Feb | Mar |
|---|---|---|---|
| Widget A | 100 | 150 | 120 |

After (unpivoted):

| Product | Month | Sales |
|---|---|---|
| Widget A | Jan | 100 |
| Widget A | Feb | 150 |
| Widget A | Mar | 120 |

### 2.2.5 Group By

Aggregates data similar to a SQL GROUP BY.

**Example**: Group a sales table by "Region" and sum the "Revenue" column.

Result: One row per region with total revenue.

### 2.2.6 Merge Queries (Joins)

Combines two tables based on a common column — equivalent to SQL JOINs.

| Join Type | Description |
|---|---|
| **Left Outer** | All rows from left table + matching from right |
| **Right Outer** | All rows from right table + matching from left |
| **Full Outer** | All rows from both tables |
| **Inner** | Only matching rows from both tables |
| **Left Anti** | Rows in left table NOT in right table |
| **Right Anti** | Rows in right table NOT in left table |

### 2.2.7 Append Queries

Stacks two or more tables on top of each other (like SQL UNION ALL). Used when you have the same structure across multiple files (e.g., monthly sales files).

---

## 2.3 The M Language (Overview)

Every step in Power Query generates M code. You can view and edit it via:
**Home → Advanced Editor**

```m
// Example M code: Load an Excel file and filter rows
let
    Source = Excel.Workbook(File.Contents("C:\Sales.xlsx"), null, true),
    Sheet1 = Source{[Item="Sheet1",Kind="Sheet"]}[Data],
    PromotedHeaders = Table.PromoteHeaders(Sheet1, [PromoteAllScalars=true]),
    FilteredRows = Table.SelectRows(PromotedHeaders, each [Revenue] > 1000)
in
    FilteredRows
```

---

## 2.4 Best Practices in Power Query

1. **Rename queries** meaningfully — avoid "Sheet1", "Query1"
2. **Remove unnecessary columns early** — reduces model size
3. **Set correct data types** for every column
4. **Avoid loading helper/staging queries** — disable their load to the model
5. **Use Parameters** for dynamic file paths or server names
6. **Document steps** with meaningful step names in Applied Steps

---

# Module 3 — Data Modeling & Relationships

## 3.1 Why Data Modeling Matters

A good data model is the foundation of an accurate and performant Power BI report. Poor modeling leads to incorrect calculations, slow performance, and confusing reports.

Power BI uses an **in-memory columnar database** called **VertiPaq** to store imported data. This engine is optimized for specific model patterns.

---

## 3.2 Star Schema vs. Flat Table

### Flat Table (Avoid)
Everything in one table. Easy to start but causes:
- Redundant data
- Slow performance
- Difficult DAX calculations

### Star Schema (Best Practice)

The **Star Schema** separates data into:

- **Fact Tables**: Contain measurable events (Sales, Transactions, Inventory). Usually has many rows and numeric values.
- **Dimension Tables**: Describe the context (Customers, Products, Dates, Regions). Usually small with descriptive attributes.

```
                    ┌──────────────┐
                    │  DimDate     │
                    │  (Date table)│
                    └──────┬───────┘
                           │
┌──────────────┐    ┌──────┴───────┐    ┌──────────────┐
│  DimCustomer │────│  FactSales   │────│  DimProduct  │
│              │    │              │    │              │
└──────────────┘    └──────┬───────┘    └──────────────┘
                           │
                    ┌──────┴───────┐
                    │  DimRegion   │
                    └──────────────┘
```

The fact table sits in the center; dimensions radiate outward like a star.

---

## 3.3 Relationships

### Relationship Properties

Every relationship in Power BI has:

| Property | Options |
|---|---|
| **Cardinality** | One-to-Many (1:*), Many-to-One (*:1), One-to-One (1:1), Many-to-Many (*:*) |
| **Cross-filter Direction** | Single, Both |
| **Active/Inactive** | Only one active relationship between two tables at a time |

### One-to-Many (Most Common)

The primary key in the dimension table (unique values) relates to a foreign key in the fact table (repeated values).

```
DimProduct[ProductID]   →   FactSales[ProductID]
  1 (unique)                    * (many rows per product)
```

**Rule**: Always join from the "one" side (dimension) to the "many" side (fact).

### Many-to-Many Relationships

Occur when neither side has unique values. Use with caution — they can cause ambiguous filter propagation. Best resolved by introducing a bridge table.

### Cross-filter Direction

- **Single**: Filters flow from dimension → fact (standard, recommended)
- **Both**: Filters flow in both directions (use sparingly — can cause circular dependencies and unexpected results)

---

## 3.4 The Date Table

A proper date table is **mandatory** for time intelligence DAX functions (year-over-year, month-to-date, etc.).

### Requirements for a Date Table

1. Contains one row for every date in the range of your data
2. Has no gaps
3. Must be marked as a **Date Table** in Power BI (Modeling → Mark as Date Table)
4. The date column must be of type **Date** with no duplicates

### Creating a Date Table in DAX

```dax
DimDate = 
ADDCOLUMNS(
    CALENDAR(DATE(2020,1,1), DATE(2026,12,31)),
    "Year",         YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month Name",   FORMAT([Date], "MMMM"),
    "Quarter",      "Q" & QUARTER([Date]),
    "Week Number",  WEEKNUM([Date]),
    "Day of Week",  FORMAT([Date], "dddd"),
    "Is Weekend",   IF(WEEKDAY([Date], 2) >= 6, TRUE, FALSE),
    "Year-Month",   FORMAT([Date], "YYYY-MM")
)
```

---

## 3.5 Calculated Columns vs. Measures

This is one of the most important concepts in Power BI.

| Feature | Calculated Column | Measure |
|---|---|---|
| **Evaluated** | Row by row at refresh time | At query time (on demand) |
| **Stored** | Yes — takes up memory | No — computed dynamically |
| **Context** | Row context | Filter context |
| **Used for** | Categorizations, flags, lookups | Aggregations, KPIs, dynamic values |
| **Visible in** | Rows of the table | Values area of visuals |

**Rule of thumb**: Use measures for anything you want to aggregate or display in a visual value. Use calculated columns for static classifications.

---

# Module 4 — DAX (Data Analysis Expressions)

## 4.1 What Is DAX?

**DAX (Data Analysis Expressions)** is the formula language used in Power BI, Analysis Services, and Power Pivot. It was designed to work with tabular data models and is used to:

- Create **Measures** (dynamic aggregations)
- Create **Calculated Columns** (row-level computations)
- Create **Calculated Tables**
- Define **KPIs** and **Row-Level Security** rules

DAX is similar to Excel formulas in syntax but fundamentally different in how it evaluates data — it operates on tables and columns, not individual cells.

---

## 4.2 Key Concepts in DAX

### 4.2.1 Evaluation Context

The most critical concept in DAX. Every DAX expression is evaluated within a **context** that determines which rows are included in the calculation.

#### Filter Context

Comes from slicers, filters, rows/columns in a matrix, or explicit CALCULATE filters. It restricts which rows are considered.

**Example**: When a slicer is set to "2024", all measures automatically calculate only for 2024 data.

#### Row Context

Exists inside calculated columns and iterator functions (SUMX, AVERAGEX, etc.). It means DAX evaluates the expression once per row of the current table.

**Example**: In a calculated column `[Profit] = [Revenue] - [Cost]`, DAX evaluates this formula for each row individually.

#### Context Transition

When CALCULATE is called inside a row context (e.g., inside an iterator), it converts the row context into an equivalent filter context. This is a powerful and advanced concept.

---

### 4.2.2 CALCULATE — The Most Important DAX Function

`CALCULATE` modifies the filter context. It is the engine behind almost every advanced DAX calculation.

**Syntax:**
```dax
CALCULATE(<expression>, <filter1>, <filter2>, ...)
```

**Definition**: Evaluates an expression in a modified filter context. Filters can add, replace, or remove existing filters.

**Example 1 — Filter to specific category:**
```dax
Electronics Sales = 
CALCULATE(
    SUM(FactSales[Revenue]),
    DimProduct[Category] = "Electronics"
)
```

**Example 2 — Remove all filters (ALL):**
```dax
Total Sales All Time = 
CALCULATE(
    SUM(FactSales[Revenue]),
    ALL(FactSales)
)
```

**Example 3 — Multiple filters:**
```dax
North Electronics 2024 = 
CALCULATE(
    SUM(FactSales[Revenue]),
    DimRegion[Region] = "North",
    DimProduct[Category] = "Electronics",
    DimDate[Year] = 2024
)
```

---

## 4.3 Beginner DAX Functions

### 4.3.1 Aggregation Functions

These are the most basic DAX functions.

---

#### SUM

**Definition**: Returns the sum of all values in a column.

**Syntax:**
```dax
SUM(<column>)
```

**Example:**
```dax
Total Revenue = SUM(FactSales[Revenue])
```

---

#### AVERAGE

**Definition**: Returns the arithmetic mean of all values in a column.

**Syntax:**
```dax
AVERAGE(<column>)
```

**Example:**
```dax
Average Order Value = AVERAGE(FactSales[OrderAmount])
```

---

#### COUNT

**Definition**: Counts the number of rows in a column that contain non-blank numeric values.

**Syntax:**
```dax
COUNT(<column>)
```

**Example:**
```dax
Number of Transactions = COUNT(FactSales[OrderID])
```

---

#### COUNTA

**Definition**: Counts the number of non-blank values in a column (works for any data type, including text).

**Syntax:**
```dax
COUNTA(<column>)
```

**Example:**
```dax
Customer Count = COUNTA(DimCustomer[CustomerName])
```

---

#### COUNTROWS

**Definition**: Counts the number of rows in a table.

**Syntax:**
```dax
COUNTROWS(<table>)
```

**Example:**
```dax
Order Count = COUNTROWS(FactSales)
```

---

#### DISTINCTCOUNT

**Definition**: Counts the number of distinct (unique) values in a column.

**Syntax:**
```dax
DISTINCTCOUNT(<column>)
```

**Example:**
```dax
Unique Customers = DISTINCTCOUNT(FactSales[CustomerID])
```

---

#### MIN / MAX

**Definition**: Returns the minimum or maximum value in a column.

**Syntax:**
```dax
MIN(<column>)
MAX(<column>)
```

**Example:**
```dax
Earliest Sale Date = MIN(FactSales[OrderDate])
Largest Order = MAX(FactSales[OrderAmount])
```

---

### 4.3.2 Logical Functions

---

#### IF

**Definition**: Returns one value if a condition is true, and another value if it is false.

**Syntax:**
```dax
IF(<logical_test>, <value_if_true>, <value_if_false>)
```

**Example:**
```dax
Sales Status = 
IF(
    [Total Revenue] >= 100000,
    "Target Met",
    "Below Target"
)
```

---

#### AND / OR

**Definition**: Logical AND/OR operators for combining conditions.

**Syntax:**
```dax
AND(<condition1>, <condition2>)
OR(<condition1>, <condition2>)
```

**Example:**
```dax
High Value Customer = 
IF(
    AND([Total Revenue] > 50000, [Order Count] > 10),
    "High Value",
    "Standard"
)
```

---

#### NOT

**Definition**: Reverses a logical condition (TRUE becomes FALSE, FALSE becomes TRUE).

**Syntax:**
```dax
NOT(<condition>)
```

**Example:**
```dax
Not Electronics = NOT(DimProduct[Category] = "Electronics")
```

---

#### SWITCH

**Definition**: Evaluates an expression against a list of values and returns the result for the first match. More readable than nested IFs.

**Syntax:**
```dax
SWITCH(<expression>, <value1>, <result1>, <value2>, <result2>, ..., [<else>])
```

**Example:**
```dax
Quarter Label = 
SWITCH(
    MONTH([Date]),
    1,  "Q1", 2,  "Q1", 3,  "Q1",
    4,  "Q2", 5,  "Q2", 6,  "Q2",
    7,  "Q3", 8,  "Q3", 9,  "Q3",
    10, "Q4", 11, "Q4", 12, "Q4"
)
```

**SWITCH TRUE pattern** (evaluate conditions):
```dax
Revenue Tier = 
SWITCH(
    TRUE(),
    [Total Revenue] >= 1000000, "Platinum",
    [Total Revenue] >= 500000,  "Gold",
    [Total Revenue] >= 100000,  "Silver",
    "Bronze"
)
```

---

#### IFERROR

**Definition**: Returns an alternative value if an expression produces an error.

**Syntax:**
```dax
IFERROR(<value>, <value_if_error>)
```

**Example:**
```dax
Safe Division = IFERROR(DIVIDE([Revenue], [Units]), 0)
```

---

#### ISBLANK

**Definition**: Returns TRUE if the value is blank.

**Syntax:**
```dax
ISBLANK(<value>)
```

**Example:**
```dax
Has Email = IF(ISBLANK(DimCustomer[Email]), "No", "Yes")
```

---

### 4.3.3 Text Functions

---

#### CONCATENATE / &

**Definition**: Joins two or more text strings together.

**Syntax:**
```dax
CONCATENATE(<text1>, <text2>)
-- Or using the & operator (preferred):
<text1> & <text2>
```

**Example:**
```dax
Full Name = DimCustomer[FirstName] & " " & DimCustomer[LastName]
```

---

#### LEFT / RIGHT / MID

**Definition**: Extracts characters from the left, right, or middle of a text string.

**Syntax:**
```dax
LEFT(<text>, <num_chars>)
RIGHT(<text>, <num_chars>)
MID(<text>, <start_position>, <num_chars>)
```

**Example:**
```dax
Area Code = LEFT(DimCustomer[Phone], 3)
Last 4 Digits = RIGHT(DimCustomer[AccountNumber], 4)
Department Code = MID(DimEmployee[EmployeeID], 3, 2)
```

---

#### LEN

**Definition**: Returns the number of characters in a text string.

**Syntax:**
```dax
LEN(<text>)
```

**Example:**
```dax
Description Length = LEN(DimProduct[Description])
```

---

#### UPPER / LOWER / PROPER

**Definition**: Converts text to all uppercase, all lowercase, or title case (first letter of each word capitalized).

**Syntax:**
```dax
UPPER(<text>)
LOWER(<text>)
PROPER(<text>)
```

**Example:**
```dax
Standardized Name = PROPER(LOWER(DimCustomer[FullName]))
```

---

#### TRIM

**Definition**: Removes all leading and trailing spaces from a text string.

**Syntax:**
```dax
TRIM(<text>)
```

**Example:**
```dax
Clean Category = TRIM(DimProduct[Category])
```

---

#### FIND / SEARCH

**Definition**: Returns the starting position of one text string within another. FIND is case-sensitive; SEARCH is not.

**Syntax:**
```dax
FIND(<find_text>, <within_text>, [<start_pos>], [<not_found_value>])
SEARCH(<find_text>, <within_text>, [<start_pos>], [<not_found_value>])
```

**Example:**
```dax
At Symbol Position = FIND("@", DimCustomer[Email], 1, 0)
```

---

#### SUBSTITUTE / REPLACE

**Definition**: SUBSTITUTE replaces all occurrences of a text with new text. REPLACE replaces text at a specific position.

**Syntax:**
```dax
SUBSTITUTE(<text>, <old_text>, <new_text>, [<instance_num>])
REPLACE(<old_text>, <start_pos>, <num_chars>, <new_text>)
```

**Example:**
```dax
Clean Phone = SUBSTITUTE(DimCustomer[Phone], "-", "")
```

---

#### FORMAT

**Definition**: Converts a value to text with a specified format.

**Syntax:**
```dax
FORMAT(<value>, <format_string>)
```

**Example:**
```dax
Revenue Formatted = FORMAT([Total Revenue], "$#,##0.00")
Month Year = FORMAT(DimDate[Date], "MMM YYYY")
```

---

### 4.3.4 Date & Time Functions

---

#### TODAY / NOW

**Definition**: Returns the current date (TODAY) or current date and time (NOW).

**Syntax:**
```dax
TODAY()
NOW()
```

**Example:**
```dax
Days Since Last Sale = DATEDIFF(MAX(FactSales[OrderDate]), TODAY(), DAY)
```

---

#### DATE

**Definition**: Creates a date from year, month, and day values.

**Syntax:**
```dax
DATE(<year>, <month>, <day>)
```

**Example:**
```dax
Year Start = DATE(YEAR(TODAY()), 1, 1)
```

---

#### YEAR / MONTH / DAY

**Definition**: Extracts the year, month number, or day number from a date.

**Syntax:**
```dax
YEAR(<date>)
MONTH(<date>)
DAY(<date>)
```

**Example:**
```dax
Sale Year = YEAR(FactSales[OrderDate])
Sale Month = MONTH(FactSales[OrderDate])
```

---

#### WEEKDAY / WEEKNUM

**Definition**: Returns the day of the week (as a number) or the week number of the year.

**Syntax:**
```dax
WEEKDAY(<date>, [<return_type>])
WEEKNUM(<date>, [<return_type>])
```

**Example:**
```dax
Day of Week Num = WEEKDAY(DimDate[Date], 2) -- Monday=1
Week Number = WEEKNUM(DimDate[Date], 2)
```

---

#### DATEDIFF

**Definition**: Returns the number of intervals between two dates.

**Syntax:**
```dax
DATEDIFF(<start_date>, <end_date>, <interval>)
-- Interval options: SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, QUARTER, YEAR
```

**Example:**
```dax
Customer Age Days = DATEDIFF(DimCustomer[SignupDate], TODAY(), DAY)
Tenure Years = DATEDIFF(DimEmployee[HireDate], TODAY(), YEAR)
```

---

#### EOMONTH

**Definition**: Returns the last day of the month, a specified number of months before or after a start date.

**Syntax:**
```dax
EOMONTH(<start_date>, <months>)
```

**Example:**
```dax
End of This Month = EOMONTH(TODAY(), 0)
End of Last Month = EOMONTH(TODAY(), -1)
```

---

## 4.4 Intermediate DAX Functions

### 4.4.1 Filter Functions

---

#### ALL

**Definition**: Returns all rows of a table or all values of a column, ignoring any filters that might have been applied. Used inside CALCULATE to remove filters.

**Syntax:**
```dax
ALL(<table_or_column>)
```

**Example — Percentage of total:**
```dax
% of Total Sales = 
DIVIDE(
    SUM(FactSales[Revenue]),
    CALCULATE(SUM(FactSales[Revenue]), ALL(FactSales))
)
```

---

#### ALLEXCEPT

**Definition**: Removes all filters from a table except the filters on the specified columns.

**Syntax:**
```dax
ALLEXCEPT(<table>, <column1>, <column2>, ...)
```

**Example:**
```dax
% of Category Sales = 
DIVIDE(
    SUM(FactSales[Revenue]),
    CALCULATE(SUM(FactSales[Revenue]), ALLEXCEPT(DimProduct, DimProduct[Category]))
)
```

---

#### ALLSELECTED

**Definition**: Returns all rows in a table or all values in a column that are within the current query's filter context but ignoring visual-level filters (preserves slicer filters but ignores visual filters).

**Syntax:**
```dax
ALLSELECTED(<table_or_column>)
```

**Example:**
```dax
% of Selected Total = 
DIVIDE(
    SUM(FactSales[Revenue]),
    CALCULATE(SUM(FactSales[Revenue]), ALLSELECTED(FactSales))
)
```

---

#### FILTER

**Definition**: Returns a table that represents a subset of another table, based on a filter condition. Often used inside CALCULATE or as a table argument.

**Syntax:**
```dax
FILTER(<table>, <filter_expression>)
```

**Example:**
```dax
High Value Orders = 
CALCULATE(
    COUNT(FactSales[OrderID]),
    FILTER(FactSales, FactSales[OrderAmount] > 5000)
)
```

---

#### KEEPFILTERS

**Definition**: Modifies how CALCULATE applies filters — instead of replacing existing filters, it intersects them (keeps both the new filter and the existing filters).

**Syntax:**
```dax
KEEPFILTERS(<filter_expression>)
```

**Example:**
```dax
Electronics in Context = 
CALCULATE(
    SUM(FactSales[Revenue]),
    KEEPFILTERS(DimProduct[Category] = "Electronics")
)
```

---

#### REMOVEFILTERS

**Definition**: Removes filters from specified columns or tables. Equivalent to ALL() inside CALCULATE, but more explicit.

**Syntax:**
```dax
REMOVEFILTERS([<table_or_column>])
```

**Example:**
```dax
Total Ignoring Region = 
CALCULATE(
    SUM(FactSales[Revenue]),
    REMOVEFILTERS(DimRegion)
)
```

---

#### VALUES

**Definition**: Returns a single-column table containing the distinct values of a specified column, respecting the current filter context.

**Syntax:**
```dax
VALUES(<column_or_table>)
```

**Example:**
```dax
Selected Regions = CONCATENATEX(VALUES(DimRegion[Region]), DimRegion[Region], ", ")
```

---

#### HASONEVALUE

**Definition**: Returns TRUE when the specified column has been filtered down to one distinct value.

**Syntax:**
```dax
HASONEVALUE(<column>)
```

**Example:**
```dax
Single Region Label = 
IF(
    HASONEVALUE(DimRegion[Region]),
    VALUES(DimRegion[Region]),
    "Multiple Regions"
)
```

---

#### SELECTEDVALUE

**Definition**: Returns the value of a column when it is filtered to a single value, otherwise returns the alternate result.

**Syntax:**
```dax
SELECTEDVALUE(<column>, [<alternate_result>])
```

**Example:**
```dax
Selected Year = SELECTEDVALUE(DimDate[Year], "All Years")
```

---

### 4.4.2 Table Functions

---

#### SUMMARIZE

**Definition**: Creates a summary table by grouping rows by specified columns and optionally adding aggregations.

**Syntax:**
```dax
SUMMARIZE(<table>, <group_by_col1>, <group_by_col2>, ..., [<name>, <expression>], ...)
```

**Example:**
```dax
Sales by Category = 
SUMMARIZE(
    FactSales,
    DimProduct[Category],
    "Total Revenue", SUM(FactSales[Revenue]),
    "Order Count",   COUNTROWS(FactSales)
)
```

---

#### ADDCOLUMNS

**Definition**: Returns a table with new columns added. Similar to SUMMARIZE but adds columns without grouping.

**Syntax:**
```dax
ADDCOLUMNS(<table>, <name>, <expression>, ...)
```

**Example:**
```dax
Products with Margin = 
ADDCOLUMNS(
    DimProduct,
    "Revenue", [Total Revenue],
    "Profit Margin", DIVIDE([Total Profit], [Total Revenue])
)
```

---

#### SELECTCOLUMNS

**Definition**: Returns a table with only specific columns selected (and optionally renamed).

**Syntax:**
```dax
SELECTCOLUMNS(<table>, <name>, <expression>, ...)
```

**Example:**
```dax
Customer Summary = 
SELECTCOLUMNS(
    DimCustomer,
    "Customer ID",   DimCustomer[CustomerID],
    "Name",          DimCustomer[FullName],
    "Country",       DimCustomer[Country]
)
```

---

#### CROSSJOIN

**Definition**: Returns a table that is the Cartesian product of all combinations of rows from two or more tables.

**Syntax:**
```dax
CROSSJOIN(<table1>, <table2>, ...)
```

**Example:**
```dax
All Combinations = CROSSJOIN(VALUES(DimProduct[Category]), VALUES(DimRegion[Region]))
```

---

#### UNION

**Definition**: Returns a table that is the union (combined rows) of two or more tables with the same number of columns.

**Syntax:**
```dax
UNION(<table1>, <table2>, ...)
```

**Example:**
```dax
All Customers = UNION(DimCustomerOnline, DimCustomerOffline)
```

---

#### INTERSECT

**Definition**: Returns the rows from one table that also appear in another table (left semi-join).

**Syntax:**
```dax
INTERSECT(<table1>, <table2>)
```

---

#### EXCEPT

**Definition**: Returns the rows from the first table that do not appear in the second table.

**Syntax:**
```dax
EXCEPT(<table1>, <table2>)
```

---

#### TOPN

**Definition**: Returns the top N rows of a table based on a specified expression.

**Syntax:**
```dax
TOPN(<n_value>, <table>, <order_by_expression>, [<order>], ...)
```

**Example:**
```dax
Top 10 Products = TOPN(10, DimProduct, [Total Revenue], DESC)
```

---

#### ROW

**Definition**: Returns a single-row table with specified column names and values.

**Syntax:**
```dax
ROW(<name1>, <expression1>, <name2>, <expression2>, ...)
```

**Example:**
```dax
KPI Summary = 
ROW(
    "Total Revenue", [Total Revenue],
    "Total Orders",  [Order Count],
    "Avg Order",     [Average Order Value]
)
```

---

### 4.4.3 Lookup & Relationship Functions

---

#### RELATED

**Definition**: Returns a related value from another table by traversing a many-to-one relationship. Used in calculated columns.

**Syntax:**
```dax
RELATED(<column>)
```

**Example (in FactSales calculated column):**
```dax
Product Category = RELATED(DimProduct[Category])
```

---

#### RELATEDTABLE

**Definition**: Returns a table of all related rows from another table. Used in calculated columns on the "one" side to get rows from the "many" side.

**Syntax:**
```dax
RELATEDTABLE(<table>)
```

**Example (in DimCustomer calculated column):**
```dax
Customer Order Count = COUNTROWS(RELATEDTABLE(FactSales))
```

---

#### LOOKUPVALUE

**Definition**: Returns the value of a column from a row that matches specified criteria. Works without a formal relationship.

**Syntax:**
```dax
LOOKUPVALUE(
    <result_column>,
    <search_column1>, <search_value1>,
    [<search_column2>, <search_value2>],
    [<alternate_result>]
)
```

**Example:**
```dax
Product Price = 
LOOKUPVALUE(
    DimProduct[UnitPrice],
    DimProduct[ProductID], FactSales[ProductID]
)
```

---

#### USERELATIONSHIP

**Definition**: Activates an inactive relationship for the duration of a CALCULATE expression.

**Syntax:**
```dax
USERELATIONSHIP(<column1>, <column2>)
```

**Example (when FactSales has both OrderDate and ShipDate related to DimDate):**
```dax
Sales by Ship Date = 
CALCULATE(
    SUM(FactSales[Revenue]),
    USERELATIONSHIP(FactSales[ShipDate], DimDate[Date])
)
```

---

#### TREATAS

**Definition**: Applies the values of a table expression as filters to columns from an unrelated table, treating one column as if it were another.

**Syntax:**
```dax
TREATAS(<table_expression>, <column1>, <column2>, ...)
```

**Example:**
```dax
Sales for Virtual Segment = 
CALCULATE(
    SUM(FactSales[Revenue]),
    TREATAS({"Electronics", "Software"}, DimProduct[Category])
)
```

---

### 4.4.4 Iterator Functions (X Functions)

Iterator functions iterate over each row of a table, evaluate an expression, and then aggregate the results. They combine row context and aggregation in one step.

---

#### SUMX

**Definition**: Evaluates an expression for each row of a table and returns the sum of all results.

**Syntax:**
```dax
SUMX(<table>, <expression>)
```

**Example:**
```dax
Total Revenue = SUMX(FactSales, FactSales[Quantity] * FactSales[UnitPrice])

-- Equivalent but cleaner than a calculated column approach
Weighted Revenue = SUMX(FactSales, FactSales[Quantity] * RELATED(DimProduct[UnitPrice]))
```

---

#### AVERAGEX

**Definition**: Evaluates an expression for each row of a table and returns the average of all results.

**Syntax:**
```dax
AVERAGEX(<table>, <expression>)
```

**Example:**
```dax
Average Profit per Order = AVERAGEX(FactSales, FactSales[Revenue] - FactSales[Cost])
```

---

#### COUNTX

**Definition**: Counts the number of rows in a table for which the specified expression evaluates to a non-blank value.

**Syntax:**
```dax
COUNTX(<table>, <expression>)
```

---

#### MAXX / MINX

**Definition**: Returns the maximum or minimum value from an expression evaluated across each row of a table.

**Syntax:**
```dax
MAXX(<table>, <expression>)
MINX(<table>, <expression>)
```

**Example:**
```dax
Max Profit per Order = MAXX(FactSales, FactSales[Revenue] - FactSales[Cost])
```

---

#### RANKX

**Definition**: Returns the rank of a value in a list of values, evaluated across a table.

**Syntax:**
```dax
RANKX(<table>, <expression>, [<value>], [<order>], [<ties>])
```

**Parameters:**
- `<order>`: ASC (ascending, 1 = smallest) or DESC (descending, 1 = largest)
- `<ties>`: Skip, Dense

**Example:**
```dax
Product Revenue Rank = 
RANKX(
    ALL(DimProduct[ProductName]),
    [Total Revenue],
    ,
    DESC,
    Dense
)
```

---

#### CONCATENATEX

**Definition**: Evaluates an expression for each row in a table and returns the concatenated string of all results, separated by a delimiter.

**Syntax:**
```dax
CONCATENATEX(<table>, <expression>, [<delimiter>], [<order_by>], [<order>])
```

**Example:**
```dax
Selected Products List = 
CONCATENATEX(
    VALUES(DimProduct[ProductName]),
    DimProduct[ProductName],
    ", ",
    DimProduct[ProductName],
    ASC
)
```

---

#### GENERATE / GENERATEALL

**Definition**: Returns a table that is the result of applying a row context to each row of the first table and expanding with the second table expression.

**Syntax:**
```dax
GENERATE(<table1>, <table2>)
```

---

# Module 5 — Advanced DAX & Analytics

## 5.1 Time Intelligence Functions

Time intelligence functions require a proper Date Table marked as such in Power BI.

---

### DATEADD

**Definition**: Returns a table containing dates shifted by a specified number of intervals.

**Syntax:**
```dax
DATEADD(<dates_column>, <number_of_intervals>, <interval>)
-- Interval: DAY, MONTH, QUARTER, YEAR
```

**Example — Prior Year Sales:**
```dax
Prior Year Revenue = 
CALCULATE(
    SUM(FactSales[Revenue]),
    DATEADD(DimDate[Date], -1, YEAR)
)
```

---

### SAMEPERIODLASTYEAR

**Definition**: Returns a table containing dates from the same period in the previous year.

**Syntax:**
```dax
SAMEPERIODLASTYEAR(<dates_column>)
```

**Example:**
```dax
Last Year Revenue = 
CALCULATE(
    SUM(FactSales[Revenue]),
    SAMEPERIODLASTYEAR(DimDate[Date])
)

YoY Growth % = 
DIVIDE(
    [Total Revenue] - [Last Year Revenue],
    [Last Year Revenue]
)
```

---

### PREVIOUSMONTH / PREVIOUSQUARTER / PREVIOUSYEAR

**Definition**: Returns a set of dates from the previous month, quarter, or year relative to the current context.

**Syntax:**
```dax
PREVIOUSMONTH(<dates_column>)
PREVIOUSQUARTER(<dates_column>)
PREVIOUSYEAR(<dates_column>)
```

**Example:**
```dax
Last Month Revenue = CALCULATE([Total Revenue], PREVIOUSMONTH(DimDate[Date]))
MoM Change = [Total Revenue] - [Last Month Revenue]
```

---

### DATESMTD / DATESQTD / DATESYTD

**Definition**: Returns a table containing the dates for the month-to-date (MTD), quarter-to-date (QTD), or year-to-date (YTD) period.

**Syntax:**
```dax
DATESMTD(<dates_column>)
DATESQTD(<dates_column>)
DATESYTD(<dates_column>, [<year_end_date>])
```

**Example:**
```dax
MTD Revenue = CALCULATE([Total Revenue], DATESMTD(DimDate[Date]))
QTD Revenue = CALCULATE([Total Revenue], DATESQTD(DimDate[Date]))
YTD Revenue = CALCULATE([Total Revenue], DATESYTD(DimDate[Date]))

-- For fiscal year ending June 30:
Fiscal YTD = CALCULATE([Total Revenue], DATESYTD(DimDate[Date], "06-30"))
```

---

### TOTALYTD / TOTALMTD / TOTALQTD

**Definition**: Shorthand functions for year-to-date, month-to-date, and quarter-to-date calculations.

**Syntax:**
```dax
TOTALYTD(<expression>, <dates_column>, [<filter>], [<year_end_date>])
```

**Example:**
```dax
YTD Revenue v2 = TOTALYTD(SUM(FactSales[Revenue]), DimDate[Date])
-- Equivalent to the DATESYTD example above
```

---

### DATESBETWEEN

**Definition**: Returns a table containing dates between two specified dates.

**Syntax:**
```dax
DATESBETWEEN(<dates_column>, <start_date>, <end_date>)
```

**Example:**
```dax
Q3 Revenue = 
CALCULATE(
    SUM(FactSales[Revenue]),
    DATESBETWEEN(DimDate[Date], DATE(2024, 7, 1), DATE(2024, 9, 30))
)
```

---

### DATESINPERIOD

**Definition**: Returns a table containing dates for a period, starting or ending from a specific date.

**Syntax:**
```dax
DATESINPERIOD(<dates_column>, <start_date>, <number_of_intervals>, <interval>)
```

**Example — Rolling 12 months:**
```dax
Rolling 12M Revenue = 
CALCULATE(
    SUM(FactSales[Revenue]),
    DATESINPERIOD(DimDate[Date], LASTDATE(DimDate[Date]), -12, MONTH)
)
```

---

### FIRSTDATE / LASTDATE

**Definition**: Returns the first or last date in the current filter context.

**Syntax:**
```dax
FIRSTDATE(<dates_column>)
LASTDATE(<dates_column>)
```

**Example:**
```dax
Period End = LASTDATE(DimDate[Date])
Period Start = FIRSTDATE(DimDate[Date])
```

---

### PARALLELPERIOD

**Definition**: Returns a table of dates parallel to those in a specified column, shifted by the given number of intervals. Unlike DATEADD, it always returns full periods.

**Syntax:**
```dax
PARALLELPERIOD(<dates_column>, <number_of_intervals>, <interval>)
```

**Example:**
```dax
Same Quarter Last Year = 
CALCULATE(
    SUM(FactSales[Revenue]),
    PARALLELPERIOD(DimDate[Date], -1, YEAR)
)
```

---

## 5.2 Advanced Filter Patterns

### The ALL + DIVIDE Pattern (% of Total)

```dax
% of Total Revenue = 
VAR CurrentRevenue = SUM(FactSales[Revenue])
VAR TotalRevenue = CALCULATE(SUM(FactSales[Revenue]), ALL(FactSales))
RETURN
DIVIDE(CurrentRevenue, TotalRevenue, 0)
```

---

### Cumulative Total (Running Sum)

```dax
Cumulative Revenue = 
CALCULATE(
    SUM(FactSales[Revenue]),
    FILTER(
        ALL(DimDate[Date]),
        DimDate[Date] <= MAX(DimDate[Date])
    )
)
```

---

### Dynamic Segmentation with SWITCH TRUE

```dax
Customer Segment = 
SWITCH(
    TRUE(),
    [Customer Revenue] >= 100000, "Enterprise",
    [Customer Revenue] >= 25000,  "Mid-Market",
    [Customer Revenue] >= 5000,   "SMB",
    "Micro"
)
```

---

### Dynamic Measure Selection (What-If Parameter)

Create a What-If Parameter in Power BI (Modeling → New Parameter), then use:

```dax
Selected Measure = 
SWITCH(
    SELECTEDVALUE(MeasureSelector[Measure]),
    "Revenue",      [Total Revenue],
    "Profit",       [Total Profit],
    "Orders",       [Order Count],
    "Avg Value",    [Average Order Value],
    [Total Revenue]  -- default
)
```

---

## 5.3 Variables in DAX

Variables (VAR) make DAX more readable, enable easier debugging, and can improve performance by avoiding repeated calculations.

**Syntax:**
```dax
VAR <name> = <expression>
...
RETURN <result_expression>
```

**Example — Profit Margin with Variables:**
```dax
Profit Margin % = 
VAR TotalRevenue = SUM(FactSales[Revenue])
VAR TotalCost    = SUM(FactSales[Cost])
VAR TotalProfit  = TotalRevenue - TotalCost
RETURN
IF(
    TotalRevenue = 0,
    BLANK(),
    DIVIDE(TotalProfit, TotalRevenue)
)
```

**Rules for VAR:**
- Variables are evaluated once when declared (not re-evaluated)
- Variables capture the filter context at the point of declaration
- Variables cannot be recursive
- RETURN must be at the end of the VAR block

---

## 5.4 CALCULATE Deep Dive

### Filter Arguments Behavior

CALCULATE filter arguments:

1. **Replace** existing filters on the same column (default behavior)
2. Use **KEEPFILTERS** to intersect instead
3. Use **ALL/REMOVEFILTERS** to remove existing filters
4. Use **CROSSFILTER** to change relationship filter direction temporarily

### CROSSFILTER

**Definition**: Overrides the cross-filter direction of a relationship within a CALCULATE expression.

**Syntax:**
```dax
CROSSFILTER(<column1>, <column2>, <direction>)
-- direction: NONE, ONEWAY, BOTHWAY
```

**Example:**
```dax
Products Sold in Region = 
CALCULATE(
    DISTINCTCOUNT(DimProduct[ProductID]),
    CROSSFILTER(FactSales[ProductID], DimProduct[ProductID], BOTHWAY)
)
```

---

## 5.5 Context Transition in Depth

Context transition occurs when CALCULATE is called inside a row context. It converts every column of the current row into an equivalent set of filters.

**Example — Measure called inside SUMX:**
```dax
-- This triggers context transition:
Total = SUMX(DimCustomer, [Customer Revenue])

-- [Customer Revenue] is a measure. For each row of DimCustomer,
-- SUMX creates a row context. When [Customer Revenue] calls CALCULATE internally,
-- the row context transitions to a filter context filtering to that specific customer.
```

This is why measures work correctly when used inside iterators.

---

## 5.6 Row-Level Security (RLS)

RLS restricts data access at the row level based on user identity.

### Static RLS

```dax
-- In the "Region Manager" role, filter DimRegion:
[ManagerEmail] = USERPRINCIPALNAME()
```

### Dynamic RLS

```dax
-- Filter FactSales based on user's assigned regions in a security table:
[Region] IN VALUES(SecurityTable[Region])
-- Where SecurityTable is filtered by USERPRINCIPALNAME()
```

---

## 5.7 Advanced DAX Patterns

### Moving Average (Rolling N Periods)

```dax
3 Month Moving Avg Revenue = 
VAR LastDate = LASTDATE(DimDate[Date])
VAR Last3Months = 
    DATESINPERIOD(DimDate[Date], LastDate, -3, MONTH)
RETURN
AVERAGEX(
    DISTINCT(SELECTCOLUMNS(Last3Months, "Month", EOMONTH([Date], 0))),
    CALCULATE(SUM(FactSales[Revenue]), DATESMTD(DimDate[Date]))
)
```

---

### ABC Classification

```dax
ABC Class = 
VAR ProductRevenue = [Total Revenue]
VAR AllRevenue = CALCULATE([Total Revenue], ALL(DimProduct))
VAR CumulativeRevenue = 
    SUMX(
        FILTER(
            ALL(DimProduct),
            [Total Revenue] >= ProductRevenue
        ),
        [Total Revenue]
    )
VAR CumulativePct = DIVIDE(CumulativeRevenue, AllRevenue)
RETURN
SWITCH(
    TRUE(),
    CumulativePct <= 0.80, "A",
    CumulativePct <= 0.95, "B",
    "C"
)
```

---

### New vs. Returning Customers

```dax
New Customers = 
COUNTROWS(
    FILTER(
        VALUES(FactSales[CustomerID]),
        CALCULATE(
            COUNTROWS(FactSales),
            DATESBETWEEN(DimDate[Date], BLANK(), MIN(DimDate[Date]) - 1)
        ) = 0
    )
)

Returning Customers = 
COUNTROWS(VALUES(FactSales[CustomerID])) - [New Customers]
```

---

### Pareto Analysis (Top 80%)

```dax
Is Top 80% Product = 
VAR CurrentProduct = DimProduct[ProductName]
VAR CumulativePct = 
    CALCULATE(
        DIVIDE(
            SUMX(
                FILTER(
                    ALL(DimProduct),
                    RANKX(ALL(DimProduct), [Total Revenue], , DESC, Dense) 
                    <= RANKX(ALL(DimProduct), [Total Revenue], [Total Revenue for this product], DESC, Dense)
                ),
                [Total Revenue]
            ),
            CALCULATE([Total Revenue], ALL(DimProduct))
        )
    )
RETURN IF(CumulativePct <= 0.80, "Top 80%", "Bottom 20%")
```

---

### Semi-Additive Measures (Last Value)

Used for balances, headcount, inventory — values that should not be summed across time.

```dax
Closing Balance = 
CALCULATE(
    LASTNONBLANK(
        DimDate[Date],
        SUM(FactBalance[Balance])
    ),
    ALL(DimDate[Date])
)
```

Or using LASTNONBLANKVALUE:

```dax
Closing Inventory = 
LASTNONBLANKVALUE(
    DimDate[Date],
    SUM(FactInventory[StockOnHand])
)
```

---

# Module 6 — Visualizations & Publishing

## 6.1 Choosing the Right Visual

| Data Question | Best Visual(s) |
|---|---|
| How does X compare to Y? | Bar chart, Column chart |
| How has X changed over time? | Line chart, Area chart |
| What is the proportion of X? | Pie chart, Donut chart, Treemap |
| How are two metrics related? | Scatter plot |
| Where is X located? | Map, Filled map, Shape map |
| What is the value of X vs. a target? | KPI card, Gauge, Bullet chart |
| What is the detailed breakdown? | Matrix, Table |
| What is the flow between categories? | Sankey (custom visual) |
| What is the distribution? | Histogram, Box plot |

---

## 6.2 Key Visual Features

### Conditional Formatting

Apply color rules, data bars, or icons to tables and matrices based on field values or DAX measures.

- Background color based on value ranges
- Icon sets (traffic lights, arrows)
- Data bars for quick comparison

### Drill-Through

Right-click on a data point in one page to navigate to a detail page filtered to that specific context.

**Setup**: Add fields to the "Drill-through" well in a destination page.

### Tooltips

Customize the tooltip that appears when hovering over a visual to show additional measures or even an entire report page as a rich tooltip.

### Bookmarks & Buttons

Bookmarks capture the state of a report (filters, visibility, page) at a specific moment. Combined with buttons, they enable navigation, toggle effects, and custom drill-down experiences.

### Sync Slicers

Synchronize slicers across multiple report pages so selections persist when users navigate.

---

## 6.3 DAX for Visuals — Dynamic Titles & Labels

```dax
Dynamic Chart Title = 
"Revenue by " & 
IF(HASONEVALUE(DimDate[Year]), VALUES(DimDate[Year]) & " - ", "") &
SELECTEDVALUE(DimRegion[Region], "All Regions")
```

---

## 6.4 Performance Optimization Tips

### Data Model Optimization

1. **Remove unnecessary columns** — every column uses memory
2. **Avoid high-cardinality text columns** in fact tables — use integer keys
3. **Use integer data types** for keys instead of text
4. **Avoid calculated columns** when a measure achieves the same result
5. **Disable Auto Date/Time** — it creates hidden date tables for every date column

### DAX Optimization

1. **Use variables** — avoids repeated expression evaluation
2. **Prefer DIVIDE() over /** — handles division by zero gracefully
3. **Use column references over measures** in CALCULATE filters — more efficient
4. **Avoid FILTER(ALL(...), ...)** when a simpler column filter suffices
5. **Use SUMX sparingly on large tables** — can be expensive

### Tools for Performance Analysis

- **Performance Analyzer** (View → Performance Analyzer): Records time taken for each visual to render
- **DAX Studio**: External tool for running and profiling DAX queries
- **Tabular Editor**: External tool for managing models and writing DAX

---

## 6.5 Publishing & Sharing

### Publishing to Power BI Service

1. From Power BI Desktop: **Home → Publish**
2. Select a workspace in the Power BI Service
3. The report and dataset are uploaded

### Workspaces

| Type | Description |
|---|---|
| **My Workspace** | Personal sandbox — not for team sharing |
| **App Workspace** | Collaborative team workspace |
| **Premium Workspace** | Available with Premium capacity; additional features |

### Apps

Package a workspace's reports and dashboards into a **Power BI App** and distribute to users. Apps provide a clean, user-friendly interface without exposing the workspace directly.

### Data Refresh

- Set scheduled refresh (up to 8x/day on Pro, 48x/day on Premium)
- Use a **Gateway** to refresh on-premises data sources
- **Incremental Refresh**: Only refresh new or changed data, not the entire dataset

### Row-Level Security Deployment

1. Create roles in Power BI Desktop (Modeling → Manage Roles)
2. Test with (Modeling → View as)
3. After publishing, assign users/groups to roles in Power BI Service

---

# Quick Reference — DAX Formula Cheat Sheet

## Aggregations

| Function | Syntax | Description |
|---|---|---|
| `SUM` | `SUM(column)` | Sum of numeric column |
| `AVERAGE` | `AVERAGE(column)` | Mean of numeric column |
| `COUNT` | `COUNT(column)` | Count non-blank numeric values |
| `COUNTA` | `COUNTA(column)` | Count non-blank values (any type) |
| `COUNTROWS` | `COUNTROWS(table)` | Count rows in a table |
| `DISTINCTCOUNT` | `DISTINCTCOUNT(column)` | Count unique values |
| `MIN` | `MIN(column)` | Smallest value |
| `MAX` | `MAX(column)` | Largest value |

## Filter Context Modifiers

| Function | Description |
|---|---|
| `CALCULATE(expr, filters)` | Evaluate expr in modified filter context |
| `ALL(table/column)` | Remove all filters from table or column |
| `ALLEXCEPT(table, cols)` | Remove all filters except on specified columns |
| `ALLSELECTED(table/column)` | Restore slicer-level filters only |
| `FILTER(table, condition)` | Return rows matching condition |
| `KEEPFILTERS(filter)` | Intersect new filter with existing |
| `REMOVEFILTERS(table/col)` | Explicitly remove filters |

## Time Intelligence

| Function | Description |
|---|---|
| `SAMEPERIODLASTYEAR(dates)` | Same period in prior year |
| `DATEADD(dates, n, interval)` | Shift dates by n intervals |
| `DATESMTD(dates)` | Month-to-date dates |
| `DATESQTD(dates)` | Quarter-to-date dates |
| `DATESYTD(dates, [YE])` | Year-to-date dates |
| `DATESBETWEEN(dates, s, e)` | Dates between start and end |
| `DATESINPERIOD(dates, s, n, i)` | Dates for n intervals from start |
| `PREVIOUSMONTH(dates)` | Previous month dates |
| `PREVIOUSYEAR(dates)` | Previous year dates |
| `TOTALYTD(expr, dates)` | YTD shorthand |

## Iterators (X Functions)

| Function | Description |
|---|---|
| `SUMX(table, expr)` | Sum of expr evaluated per row |
| `AVERAGEX(table, expr)` | Average of expr per row |
| `MAXX(table, expr)` | Maximum of expr per row |
| `MINX(table, expr)` | Minimum of expr per row |
| `RANKX(table, expr)` | Rank of value in table |
| `CONCATENATEX(table, expr, delim)` | Concatenate expr per row |

## Lookup & Relationships

| Function | Description |
|---|---|
| `RELATED(column)` | Value from related table (many-to-one) |
| `RELATEDTABLE(table)` | Rows from related table (one-to-many) |
| `LOOKUPVALUE(result, search, val)` | Lookup without formal relationship |
| `USERELATIONSHIP(col1, col2)` | Activate inactive relationship |
| `TREATAS(table, col)` | Apply table as filter to column |

## Logical

| Function | Description |
|---|---|
| `IF(cond, true, false)` | Conditional value |
| `SWITCH(expr, v1, r1, ..., else)` | Multi-condition switch |
| `IFERROR(expr, fallback)` | Catch errors |
| `ISBLANK(value)` | Check for blank |
| `AND(c1, c2)` | Logical AND |
| `OR(c1, c2)` | Logical OR |

## Variables

```dax
MyMeasure = 
VAR Variable1 = <expression1>
VAR Variable2 = <expression2>
RETURN
<result using Variable1, Variable2>
```

---

## 📚 Recommended Learning Path

| Stage | Topics | Estimated Time |
|---|---|---|
| **Week 1** | Modules 1–2: Interface, Power Query | 6–8 hours |
| **Week 2** | Module 3: Data Modeling, Star Schema | 4–6 hours |
| **Week 3** | Module 4: Basic to Intermediate DAX | 8–10 hours |
| **Week 4** | Module 5: Advanced DAX, Time Intelligence | 8–10 hours |
| **Week 5** | Module 6: Visuals, Performance, Publishing | 4–6 hours |
| **Ongoing** | Build real projects, use DAX Studio, practice | Continuous |

---

## 🔗 Essential Resources

- **Official Docs**: [learn.microsoft.com/power-bi](https://learn.microsoft.com/en-us/power-bi/)
- **DAX Reference**: [dax.guide](https://dax.guide)
- **DAX Patterns**: [daxpatterns.com](https://www.daxpatterns.com)
- **SQLBI (Marco & Alberto)**: [sqlbi.com](https://www.sqlbi.com)
- **DAX Studio (Free Tool)**: [daxstudio.org](https://daxstudio.org)
- **Tabular Editor (Free)**: [tabulareditor.com](https://tabulareditor.com)
- **Power BI Community**: [community.powerbi.com](https://community.powerbi.com)

---

*Course last updated: March 2026 | Compatible with Power BI Desktop (Latest)*
