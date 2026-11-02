# SQL Data Analytics Project

A collection of SQL scripts that take a sales data warehouse from first-look
exploration through to advanced analytical techniques. Each script is a
self-contained step that builds on the one before it, and together they form
a repeatable workflow for turning raw warehouse tables into business insight.

## Objectives

- Understand the structure and contents of a data warehouse before analysing it
- Profile dimensions, date ranges, and key business measures
- Answer common business questions about size, ranking, trends, and contribution
- Practise advanced SQL: window functions, CTEs, aggregations, and CASE logic

## Project Structure

```
sql-data-analytics-project/
├── scripts/
│   ├── 01_data_exploration.sql
│   ├── 02_dimensions_exploration.sql
│   ├── 03_date_range_exploration.sql
│   ├── 04_measures_exploration.sql
│   ├── 05_magnitude_analysis.sql
│   ├── 06_ranking_analysis.sql
│   ├── 07_change_over_time_analysis.sql
│   ├── 08_cumulative_analysis.sql
│   ├── 09_performance_analysis.sql
│   ├── 10_part_to_whole_analysis.sql
│   └── 11_data_segmentation.sql
└── README.md
```

## Analysis Roadmap

### Phase 1: Exploratory Data Analysis (EDA)

```
1. Data Exploration: list tables, views, and column metadata
2. Dimensions Exploration: inspect the distinct values in each dimension
3. Date Range Exploration: find the time span covered by the data
4. Measures Exploration: calculate the key business metrics and totals
```

### Phase 2: Advanced Analytics

```
1. Magnitude Analysis: compare measures across categories
2. Ranking Analysis: identify top and bottom performers
3. Change-Over-Time Analysis: track trends and seasonality
4. Cumulative Analysis: build running totals and moving averages
5. Performance Analysis: benchmark against averages and prior periods
6. Part-to-Whole Analysis: measure each category's share of the total
7. Data Segmentation: group records into meaningful segments
```

## Data Model

The scripts query a gold-layer star schema data warehouse made up of:

- **Dimension tables**: e.g. `gold.dim_customers`, `gold.dim_products`
- **Fact table**: e.g. `gold.fact_sales`

> Update this section with your actual tables and columns.

## SQL Techniques Used

- `INFORMATION_SCHEMA` metadata queries
- Aggregate functions (`SUM`, `COUNT`, `AVG`, `MIN`, `MAX`)
- Window functions (`RANK`, `ROW_NUMBER`, `LAG`, running `SUM() OVER`)
- Common Table Expressions (CTEs)
- `CASE` expressions for segmentation
- Date functions for time-based analysis

## Getting Started

1. Set up the data warehouse in SQL Server and SSMS
2. Load the dataset (see the source below)
3. Run the scripts in numerical order from the `scripts/` folder

## Key Findings

> Add a few bullet points from your own results, for example top-performing
> categories, growth trends, or customer segments.

## Tech Stack

- SQL Server and SSMS
- Git and GitHub

## Credits

The dataset and overall project structure come from The Complete SQL Bootcamp by
Data with Baraa. The scripts in this repository are my own rewritten
implementations.

## Author

**Saga Mohamed**
[LinkedIn]www.linkedin.com/in/saga-mohamed-970111144
