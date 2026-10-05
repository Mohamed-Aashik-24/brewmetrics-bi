# Reflection

The BrewMetrics BI project gave me experience in developing a Business Intelligence solution using Power BI while following a version-controlled development process.

GitHub Copilot was useful during the development of the DAX measures. It helped me generate ideas and initial formulas for calculations such as month-over-month growth, running total sales, city ranking using RANKX, and average transaction value. However, the generated formulas had to be reviewed against the actual Power BI data model and tested using report visuals before being accepted.

The Running Total Sales measure was particularly useful because it required understanding how CALCULATE, FILTER, ALLSELECTED, and MAX work together. The RANKX measure also required checking that the cities were ranked correctly according to their total sales.

Using Git and GitHub changed my approach compared with a normal Power BI lab. Instead of completing the entire report first and submitting a single file, I developed the project in smaller stages. The star schema, DAX measures, dashboard, and documentation were developed and committed separately. This created a clear development history and made it possible to track how the project changed over time.

The final dashboard combines KPI cards, city analysis, monthly sales, running total sales, ranking, and interactive filters. The project helped me understand that a BI solution requires more than creating charts. Correct data modelling, DAX validation, documentation, version control, and responsible use of AI are also important parts of the development process.
