# Tutorial 2: Model Flow in This Workspace

This walkthrough explains how the current models connect.

## 1. Source-aligned staging models

The project starts by cleaning and renaming source data:

- [stg_customers.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_customers.sql) maps customer source fields
- [stg_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_orders.sql) standardizes orders and derives fields such as `valid_order_date`
- [stg_payments.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/stripe/stg_payments.sql) converts payment amounts into dollars

## 2. Fact model

[fct_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/fct_orders.sql) combines:

- orders from [stg_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_orders.sql)
- payments from [stg_payments.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/stripe/stg_payments.sql)

It aggregates successful payments by `order_id` and produces a business-ready order fact model.

## 3. Dimension model

[dim_customers.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/dim_customers.sql) joins:

- customer details from [stg_customers.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_customers.sql)
- order metrics from [fct_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/fct_orders.sql)

This produces customer-level analytics fields such as:

- first order date
- most recent order date
- number of orders
- lifetime value

## 4. How to read this project

When learning from this workspace, use this pattern:

1. open a staging model and identify renames and light transformations
2. open a mart model and find each `ref(...)`
3. trace where each dependency comes from
4. review tests and docs to see how the model is validated and described
