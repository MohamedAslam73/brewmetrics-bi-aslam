# BrewMetrics BI

## Project Overview

BrewMetrics BI is a Power BI business intelligence solution developed for BrewMetrics Coffee Co. The project analyzes coffee sales across different cities, store formats, product categories, and items.

The solution uses a version-controlled Power BI Project with GitHub and GitHub Copilot-assisted DAX development.

## Data Model

The project uses a star schema consisting of:

* **Fact_Sales** – Contains transaction-level sales data including quantity, unit price, and sales amount.
* **Dim_Date** – Contains date-related information used for time-based analysis.
* **Dim_City** – Contains city information used for city-level analysis.
* **Dim_Product** – Contains product category and item information.

## DAX Measures

### 1. Total Sales

```DAX
Total Sales =
SUM(Fact_Sales[sales_amount])
```

Calculates the total sales amount.

### 2. Month-over-Month Growth

```DAX
MoM Growth % =
VAR CurrentSales = [Total Sales]
VAR PreviousSales =
    CALCULATE(
        [Total Sales],
        DATEADD(Dim_Date[Date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentSales - PreviousSales, PreviousSales)
```

Calculates the percentage change in sales compared with the previous month.

### 3. Running Total Sales

```DAX
Running Total Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        ALL(Dim_Date[Date]),
        Dim_Date[Date] <= MAX(Dim_Date[Date])
    )
)
```

Calculates cumulative sales over time.

### 4. City Sales Rank

```DAX
City Sales Rank =
RANKX(
    ALL(Dim_City[city]),
    [Total Sales],
    ,
    DESC,
    DENSE
)
```

Ranks cities according to their total sales performance.

### 5. Average Order Value

```DAX
Average Order Value =
DIVIDE(
    [Total Sales],
    DISTINCTCOUNT(Fact_Sales[transaction_id])
)
```

Calculates the average sales value per transaction.

## Dashboard Visuals

The dashboard contains the following visuals:

### 1. Cold Brew Monthly Sales Trend

* Line chart
* Displays monthly sales performance of Cold Brew.
* Helps identify the seasonal sales pattern.

### 2. Sales Performance by City

* Column chart
* Compares total sales across cities.
* Uses the City Sales Rank measure to support ranking analysis.

### 3. Cumulative Sales Trend

* Line chart
* Uses the Running Total Sales measure.
* Shows how sales accumulate throughout the analysis period.

### 4. City Slicer

* Allows users to filter the dashboard by city.

### 5. Category Slicer

* Allows users to filter the dashboard by product category.

### 6. City → Store Format Drill-Down

* Allows users to drill from city level into store format.
* Provides more detailed performance analysis by Flagship, Kiosk, and Drive-Thru.

## Key Insights

* The dashboard allows managers to explore the seasonal Cold Brew sales pattern.
* City-level sales differences can be compared using the sales performance visual and ranking measure.
* Running total analysis provides a cumulative view of sales performance over time.
* Slicers and drill-down functionality allow users to interactively explore the sales data.

## Tools Used

* Power BI Desktop
* DAX
* GitHub
* Git
* Visual Studio Code
* GitHub Copilot

## Project Workflow

The project was developed incrementally using version control:

1. Repository and Power BI project setup
2. Star schema creation
3. Copilot-assisted DAX measure development
4. Dashboard development
5. Documentation and reflection
