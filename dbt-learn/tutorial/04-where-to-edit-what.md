# Tutorial 4: Where to Edit What

This repository is small, but it already follows the same model structure used in larger dbt projects. The key is knowing which folder to edit depending on the type of work you are doing.

## 1. If you want to clean raw data

Edit a file in:

- [models/staging/](/Users/arpanghosal/dbt/dbt-learn/models/staging)

Typical examples:

- [models/staging/jaffle_shop/stg_customers.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_customers.sql)
- [models/staging/jaffle_shop/stg_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_orders.sql)
- [models/staging/stripe/stg_payments.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/stripe/stg_payments.sql)

This is the best place for:

- renaming columns
- casting data types
- filtering rows
- deriving simple fields like `valid_order_date`

## 2. If you want to build business logic

Edit a file in:

- [models/marts/](/Users/arpanghosal/dbt/dbt-learn/models/marts)

Typical examples:

- [models/marts/core/fct_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/fct_orders.sql)
- [models/marts/core/dim_customers.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/dim_customers.sql)
- [models/marts/intermediate/int_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/intermediate/int_orders.sql)

This is where you should place:

- joins between models
- aggregations
- business metrics
- final outputs meant for reporting or downstream use

## 3. If you want to validate assumptions

Edit a file in:

- [tests/](/Users/arpanghosal/dbt/dbt-learn/tests)

Example:

- [tests/assert_stg_payments_amount_is_positive.sql](/Users/arpanghosal/dbt/dbt-learn/tests/assert_stg_payments_amount_is_positive.sql)

Use tests to enforce rules like:

- payment amounts should be positive
- no duplicate customer keys
- no null primary keys
- statuses must match a known list

## 4. If you want to adjust project-level settings

Edit:

- [dbt_project.yml](/Users/arpanghosal/dbt/dbt-learn/dbt_project.yml)

This file controls:

- project name
- model paths
- test paths
- macro paths
- default materializations

## 5. If you want to add reusable SQL logic

Edit a file in:

- [macros/](/Users/arpanghosal/dbt/dbt-learn/macros)

This is the place for logic you want to reuse across multiple models. A macro is usually a good choice when the same SQL snippet appears repeatedly.

## 6. If you want to add reference data

Edit a file in:

- [seeds/](/Users/arpanghosal/dbt/dbt-learn/seeds)

Seeds are useful for:

- small lookup tables
- reference dimension values
- static data that should be version-controlled and loaded into the warehouse

## 7. If you want to preserve point-in-time history

Edit a file in:

- [snapshots/](/Users/arpanghosal/dbt/dbt-learn/snapshots)

Snapshots are used for tracking historical changes in data over time.

## Quick rule of thumb

Use this simple checklist:

- raw cleanup or field standardization? -> staging
- business transform or aggregated metric? -> marts
- data quality rule? -> tests
- shared reusable SQL? -> macros
- static lookup data? -> seeds
- historic state tracking? -> snapshots
- project-wide config? -> dbt_project.yml

This mental model is the foundation of a maintainable dbt project.
