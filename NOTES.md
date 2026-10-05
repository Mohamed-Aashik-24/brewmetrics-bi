# Copilot-Assisted DAX Development

## 1. Total Sales

### DAX Measure

```DAX
Total Sales =
SUM(Fact_Sales[sales_amount])
```

### Description

This measure calculates the total sales generated from all sales transactions in the Fact_Sales table.

### Copilot Assistance

GitHub Copilot was used to assist in creating the basic DAX aggregation for the sales amount column.

### Final Review

The measure was checked against the Fact_Sales table and tested in Power BI to ensure that the total sales value changes correctly when filters are applied.

---

## 2. Month-over-Month Growth

### Supporting Measure

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

### DAX Measure

```DAX
MoM Growth % =
DIVIDE(
    [Total Sales] - [Previous Month Sales],
    [Previous Month Sales]
)
```

### Description

This measure calculates the percentage change in sales compared with the previous month.

### Copilot Assistance

GitHub Copilot was used to assist with the DAX logic for comparing current-month sales with previous-month sales.

### Final Review

The calculation was reviewed to ensure that the Dim_Date table was used for time-based calculations and that the measure worked correctly with the Power BI filter context.

---

## 3. Running Total Sales

### DAX Measure

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

### Description

This measure calculates cumulative sales up to the current date while respecting the selected date context.

### Copilot Assistance

GitHub Copilot was used as an assistant for developing the cumulative sales calculation.

### Final Review

The formula was tested in Power BI using a monthly line chart. The running total increases as the reporting period progresses.

The ALLSELECTED function allows the calculation to respect the current report selections, while FILTER and MAX determine the dates included in the cumulative calculation.

---

## 4. City Sales Rank

### DAX Measure

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

### Description

This measure ranks the cities according to their total sales.

The city with the highest total sales receives Rank 1.

### Copilot Assistance

GitHub Copilot was used to assist in creating the RANKX-based city ranking calculation.

### Final Review

The measure was tested using a table containing City, Total Sales, and City Sales Rank.

The final dashboard shows the following city ranking:

1. Bengaluru
2. Chennai
3. Hyderabad
4. Coimbatore

---

## 5. Average Transaction Value

### DAX Measure

```DAX
Average Transaction Value =
DIVIDE(
    [Total Sales],
    DISTINCTCOUNT(Fact_Sales[sale_id])
)
```

### Description

This measure calculates the average sales value generated per transaction.

### Copilot Assistance

GitHub Copilot was used to assist with the calculation of average transaction value.

### Final Review

The measure was tested in Power BI and displayed as a KPI card in the final dashboard.

The dashboard shows an Average Transaction Value of ₹134.15.

---

## 6. Total Quantity

### DAX Measure

```DAX
Total Quantity =
SUM(Fact_Sales[quantity])
```

### Description

This measure calculates the total quantity of products sold.

### Dashboard Usage

The measure is displayed as a KPI card in the final dashboard.

---

## DAX Development Process

The DAX development process followed these steps:

1. Identify the business requirement.
2. Use GitHub Copilot to assist with the initial DAX approach.
3. Review the generated formula.
4. Check the formula against the Power BI data model.
5. Test the measure in Power BI.
6. Make corrections when required.
7. Use the validated measure in the dashboard.
8. Commit the completed development step using Git.
