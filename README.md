# SQL Data Analytics Project

A set of SQL Server scripts that take a sales data warehouse from first-look exploration through to advanced analytical techniques. Each script is a self-contained step that builds on the previous one, together forming a repeatable workflow for turning warehouse tables into business insight.

## Objectives

- Understand the structure and contents of a data warehouse before analysing it
- Profile dimensions, date ranges, and key business measures
- Answer common business questions about size, ranking, trends, and contribution
- Practise advanced T-SQL: window functions, CTEs, date functions, and CASE logic

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

## Data Model

The scripts query a gold-layer star schema in SQL Server:

| Table | Type | Columns used |
|---|---|---|
| `gold.fact_sales` | Fact | `order_number`, `product_key`, `customer_key`, `order_date`, `sales_amount`, `quantity`, `price` |
| `gold.dim_customers` | Dimension | `customer_key`, `first_name`, `last_name`, `country`, `gender`, `birthdate` |
| `gold.dim_products` | Dimension | `product_key`, `product_name`, `category`, `subcategory`, `cost` |

`fact_sales` joins to `dim_customers` on `customer_key` and to `dim_products` on `product_key`.

## Analysis Roadmap

### Phase 1: Exploratory Data Analysis (EDA)

| # | Script | What it does |
|---|---|---|
| 01 | Data Exploration | Lists tables, views, and column metadata via `INFORMATION_SCHEMA` |
| 02 | Dimensions Exploration | Lists distinct countries and the category > subcategory > product hierarchy |
| 03 | Date Range Exploration | Finds the order history span and the customer age range |
| 04 | Measures Exploration | Calculates headline metrics: revenue, units, average price, orders, products, customers |

### Phase 2: Advanced Analytics

| # | Script | What it does |
|---|---|---|
| 05 | Magnitude Analysis | Breaks customers, products, and revenue down by country, gender, and category |
| 06 | Ranking Analysis | Finds top and bottom products and customers with `TOP N` and `RANK()` |
| 07 | Change-Over-Time Analysis | Builds monthly sales, customer, and volume trends in three different ways |
| 08 | Cumulative Analysis | Computes running totals and moving averages with window functions |
| 09 | Performance Analysis | Compares each product's yearly sales to its own average and to the prior year |
| 10 | Part-to-Whole Analysis | Calculates each category's percentage share of total revenue |
| 11 | Data Segmentation | Buckets products by cost and classifies customers as VIP, Regular, or New |

## SQL Techniques Used

- `INFORMATION_SCHEMA` metadata queries
- Aggregates: `SUM`, `COUNT`, `COUNT(DISTINCT ...)`, `AVG`, `MIN`, `MAX`
- Joins: `LEFT JOIN` between fact and dimension tables
- Window functions: `RANK() OVER`, `LAG()`, `SUM() OVER`, `AVG() OVER`, `PARTITION BY`
- Common Table Expressions (CTEs) and derived tables
- `CASE` expressions for segmentation and trend labelling
- Date functions: `DATEDIFF`, `DATETRUNC`, `FORMAT`, `YEAR`, `MONTH`, `GETDATE`
- `UNION ALL` to consolidate metrics into one report
- `COALESCE`, `CAST`, and `ROUND`

## Notes and Design Decisions

- **Order lines vs. orders:** `COUNT(order_number)` counts sales lines, while `COUNT(DISTINCT order_number)` counts actual orders. Script 04 shows both.
- **Choice of driving table:** starting a `LEFT JOIN` from the fact table only returns categories and products that have sold. Starting from the dimension also returns those that never sold (scripts 05 and 06).
- **Ties with `TOP N`:** `TOP N` returns an arbitrary subset when values tie, so script 06 also uses `RANK()` to return every tied row.
- **Sorting formatted dates:** `FORMAT()` returns text, so ordering by it sorts months alphabetically. Script 07 sorts by a true date (`DATETRUNC`) to keep calendar order.
- **Moving average frame:** the "moving average" in script 08 has no frame clause, so it is a cumulative average from the first year to the current one, not a rolling window.
- **Year-over-year edge case:** a product's first year has no prior-year value, and the `CASE` in script 09 labels it `No Change` rather than `N/A`.
- **Segmentation boundaries:** customer "lifespan" in script 11 is the gap between first and last order, so a one-time buyer is always classed as `New`.
- **Age calculation:** `DATEDIFF(YEAR, ...)` counts calendar-year boundaries crossed, so ages in script 03 can be off by one.

## Getting Started

1. Install SQL Server 2022 or later (`DATETRUNC` is not available in earlier versions) and SQL Server Management Studio (SSMS)
2. Set up the data warehouse and load the dataset (see Credits)
3. Open the scripts in the `scripts/` folder
4. Run them in numerical order

## Key Findings

> Replace this section with insights from your own runs, for example:
>
> - The top-performing category and its share of total revenue
> - The top 5 products and top 10 customers by revenue
> - Revenue trend and peak months over the period covered
> - The split of customers across VIP, Regular, and New segments
> - The number of products that never sold

## Tech Stack

- SQL Server 2022+
- SQL Server Management Studio (SSMS)
- Git and GitHub

## Credits

The dataset and overall project structure come from The Complete SQL Bootcamp by Data With Baraa. The scripts in this repository are my own rewritten implementations.

## Author

**Saga Mohamed**
[LinkedIn]www.linkedin.com/in/saga-mohamed-970111144
