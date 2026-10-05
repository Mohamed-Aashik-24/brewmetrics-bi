# BrewMetrics BI

## BrewMetrics Coffee Co. Sales & Performance Dashboard

A Business Intelligence solution developed using Power BI, DAX, GitHub, Visual Studio Code, and GitHub Copilot.

## Project Overview

BrewMetrics Coffee Co. requires a Business Intelligence solution to analyse sales performance across different cities, products, and months.

This project transforms transaction-level sales data into an interactive Power BI dashboard.

The dashboard provides information about total sales, monthly sales, running sales, city performance, city ranking, average transaction value, total quantity, and month-over-month growth.

The reporting period shown in the dashboard is April to July 2026.

## Business Objectives

The main objectives of the project are:

- Analyse overall sales performance.
- Compare sales performance across cities.
- Rank cities according to total sales.
- Analyse monthly sales trends.
- Calculate cumulative running sales.
- Calculate month-over-month sales growth.
- Calculate average transaction value.
- Analyse total quantity sold.
- Provide interactive filtering using Power BI slicers.

## Dataset

The project uses the provided:

`brewmetrics_sales.csv`

The dataset contains transaction-level sales information including:

- Date
- City
- Store Format
- Category
- Item
- Quantity
- Unit Price
- Sales Amount

The data was transformed using Power Query before being used in the Power BI data model.

## Data Model

The project uses a Star Schema.

### Fact_Sales

Fact_Sales contains the transaction-level sales data.

Important fields include:

- sale_id
- date
- city
- store_format
- category
- item
- quantity
- unit_price
- sales_amount

### Dim_Date

Dim_Date contains date-related information used for time-based analysis.

It is used for:

- Monthly analysis
- Running totals
- Month-over-month calculations
- Date filtering

### Dim_City

Dim_City contains the unique cities used for geographical sales analysis.

### Dim_Product

Dim_Product contains product and category information.

### Dim_Store

Dim_Store contains store-format information.

## DAX Measures

### Total Sales

```DAX
Total Sales =
SUM(Fact_Sales[sales_amount])
```

Calculates the total sales amount.

### Previous Month Sales

```DAX
Previous Month Sales =
CALCULATE(
    [Total Sales],
    DATEADD(
        Dim_Date[Date],
        -1,
        MONTH
    )
)
```

Calculates the sales amount for the previous month.

### Month-over-Month Growth

```DAX
MoM Growth % =
DIVIDE(
    [Total Sales] - [Previous Month Sales],
    [Previous Month Sales]
)
```

Calculates the percentage change in sales compared with the previous month.

### Running Total Sales

```DAX
Running Total Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        ALLSELECTED(Dim_Date[Date]),
        Dim_Date[Date] <= MAX(Dim_Date[Date])
    )
)
```

Calculates cumulative sales over the selected reporting period.

### City Sales Rank

```DAX
City Sales Rank =
RANKX(
    ALL(Dim_City[City]),
    [Total Sales],
    ,
    DESC,
    DENSE
)
```

Ranks cities according to total sales.

### Average Transaction Value

```DAX
Average Transaction Value =
DIVIDE(
    [Total Sales],
    DISTINCTCOUNT(Fact_Sales[sale_id])
)
```

Calculates the average revenue generated per transaction.

### Total Quantity

```DAX
Total Quantity =
SUM(Fact_Sales[quantity])
```

Calculates the total quantity sold.

## Dashboard

The final Power BI dashboard contains:

- Average Transaction Value KPI
- Total Sales KPI
- Month-over-Month Growth KPI
- Total Quantity KPI
- Total Sales by City chart
- City Sales Rank table
- Total Sales by Month chart
- Running Total Sales by Month chart
- Item slicer
- City slicer

## Dashboard Results

### Total Sales

The dashboard shows total sales of:

**₹622,460.73**

Displayed as:

**₹622.46K**

### Average Transaction Value

The dashboard shows:

**₹134.15**

### Month-over-Month Growth

The dashboard shows:

**1.12%**

### Total Quantity

The dashboard shows approximately:

**7K**

## City Performance

The dashboard shows the following city performance:

| City | Total Sales | Rank |
|---|---:|---:|
| Bengaluru | ₹182,365.47 | 1 |
| Chennai | ₹159,514.50 | 2 |
| Hyderabad | ₹147,831.93 | 3 |
| Coimbatore | ₹132,748.83 | 4 |

Bengaluru is the highest-performing city based on total sales, while Coimbatore has the lowest total sales among the four cities shown.

## Monthly Sales

The dashboard provides a monthly sales visual for:

- April
- May
- June
- July

The monthly sales visual shows relatively high sales during April, May, and June, followed by a substantial decrease in July.

## Running Total

The Running Total Sales visual shows cumulative sales increasing throughout the reporting period and reaching approximately ₹622K by July.

## Interactive Filters

The dashboard contains an Item slicer with:

- Brownie
- Cold Brew
- Mug

The dashboard also contains a City slicer with:

- Bengaluru
- Chennai
- Coimbatore
- Hyderabad

These filters allow users to interactively explore the sales data.

## Version Control

Git and GitHub were used to maintain the development history of the project.

The development process was divided into multiple stages:

1. Repository setup
2. Star schema creation
3. DAX measure development
4. Running total development
5. City ranking development
6. Additional analytical measures
7. Dashboard development
8. Documentation
9. Final dashboard export

Each major stage was committed separately so that the complete development process remains traceable.

## GitHub Copilot

GitHub Copilot was used as an AI-assisted development tool during DAX development.

Copilot suggestions were reviewed, tested, and validated against the Power BI data model before being used in the final dashboard.

The Copilot-assisted DAX development process is documented in:

`NOTES.md`

## Tools and Technologies

- Power BI Desktop
- Power Query
- DAX
- Git
- GitHub
- Visual Studio Code
- GitHub Copilot

## Project Deliverables

The project contains:

- Power BI Project (.pbip)
- Power BI Semantic Model
- Power BI Report
- README.md
- NOTES.md
- REFLECTION.md
- Final Dashboard PDF

## Conclusion

The BrewMetrics BI project converts transaction-level sales data into an interactive Business Intelligence dashboard.

The solution provides management with a clear view of overall sales, city performance, city ranking, monthly trends, cumulative sales, month-over-month growth, average transaction value, and total quantity.

Power BI and DAX provide the analytical and visual capabilities, while GitHub provides version control and GitHub Copilot supports the DAX development process.
