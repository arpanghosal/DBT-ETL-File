# Tutorial 1: Project Tour

This project follows a typical dbt layout with a small learning-oriented model graph.

## 1. Project configuration

Start with [dbt_project.yml](/Users/arpanghosal/dbt/dbt-learn/dbt_project.yml).

It defines:

- the project name: `jaffle_shop`
- where dbt looks for models, tests, seeds, macros, and snapshots
- default materialization for staging and mart models

## 2. Staging layer

The staging layer lives under [models/staging/](/Users/arpanghosal/dbt/dbt-learn/models/staging).

Examples:

- [models/staging/jaffle_shop/stg_customers.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_customers.sql)
- [models/staging/jaffle_shop/stg_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_orders.sql)
- [models/staging/stripe/stg_payments.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/stripe/stg_payments.sql)

Use this layer to:

- rename raw source columns into clearer analytics names
- perform light cleanup
- keep transformations close to the source domain

## 3. Mart layer

The mart layer lives under [models/marts/](/Users/arpanghosal/dbt/dbt-learn/models/marts).

Examples:

- [models/marts/core/fct_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/fct_orders.sql)
- [models/marts/core/dim_customers.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/dim_customers.sql)
- [models/marts/intermediate/int_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/intermediate/int_orders.sql)

This is where business-ready models are assembled from staging models.

## 4. Tests and documentation

Examples:

- test example: [tests/assert_stg_payments_amount_is_positive.sql](/Users/arpanghosal/dbt/dbt-learn/tests/assert_stg_payments_amount_is_positive.sql)
- docs block: [models/staging/jaffle_shop/jaffle_shop.md](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/jaffle_shop.md)

These files show how dbt projects mix SQL transformations with data quality and documentation.
