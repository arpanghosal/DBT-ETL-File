# Tutorial 3: Basic dbt Workflow

This section explains the basic dbt workflow in a way that matches the structure of this repository.

## 1. The dbt project lifecycle

A typical dbt workflow usually follows this sequence:

1. Define sources and models
2. Build models with `dbt run`
3. Test data quality with `dbt test`
4. Review documentation with `dbt docs generate`
5. Refresh and iterate as business logic changes

In this repo, the current project layout naturally supports that flow:

- [models/staging/](/Users/arpanghosal/dbt/dbt-learn/models/staging) holds the cleaning and standardization layer
- [models/marts/](/Users/arpanghosal/dbt/dbt-learn/models/marts) holds more final business-ready logic
- [tests/](/Users/arpanghosal/dbt/dbt-learn/tests) holds validation logic
- [dbt_project.yml](/Users/arpanghosal/dbt/dbt-learn/dbt_project.yml) tells dbt what folders to use

## 2. Core dbt commands

### `dbt run`

`dbt run` executes the models in the project.

Use it when you:

- add a new model sql file
- change logic in a staging or mart model
- want to rebuild the warehouse tables/views created by the project

In this project, running dbt will build the staging and mart models defined under the current directory structure.

### `dbt test`

`dbt test` runs the checks in the project, including generic tests and custom SQL tests.

This repo has a custom test example in [tests/assert_stg_payments_amount_is_positive.sql](/Users/arpanghosal/dbt/dbt-learn/tests/assert_stg_payments_amount_is_positive.sql).

Use this command when you want to verify:

- null rules
- positivity checks
- uniqueness or referential integrity
- custom business validations

### `dbt docs generate`

`dbt docs generate` builds the documentation site for the project.

This is useful when you want to inspect the model lineage and understand how a field is transformed from source to final table.

### `dbt build`

`dbt build` is a convenience command that runs models and tests together.

A typical sequence for learning is:

```bash
dbt build
```

This helps you validate both the transformation logic and the assumptions behind it in one pass.

## 3. How this repo maps to the workflow

### Source and raw data awareness

This repo is structured around a simple layered design:

- source data is cleaned in staging
- business logic is assembled in marts
- transformation quality is enforced with tests

This is exactly the general pattern used in production dbt projects.

### Typical edit cycle

When making a change:

1. Identify the right layer in the project
2. Edit the SQL model for that layer
3. Run `dbt build` or `dbt run` and `dbt test`
4. Check whether the output matches the expected business logic
5. Repeat until the data is trustworthy

## 4. Practical examples from this repo

For example:

- [models/staging/jaffle_shop/stg_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/staging/jaffle_shop/stg_orders.sql) is a good place to rename fields or derive simple business flags
- [models/marts/core/fct_orders.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/fct_orders.sql) is a good place to aggregate order-level logic
- [models/marts/core/dim_customers.sql](/Users/arpanghosal/dbt/dbt-learn/models/marts/core/dim_customers.sql) is where customer-level metrics are assembled
- [tests/assert_stg_payments_amount_is_positive.sql](/Users/arpanghosal/dbt/dbt-learn/tests/assert_stg_payments_amount_is_positive.sql) shows a simple quality check that protects a model from bad data

## 5. Learning habit

When you work in dbt, ask yourself these questions:

- Is this logic a source cleanup, a transformation, or a final metric?
- Which file should own this logic?
- Which other model does this model depend on?
- What test should protect this change?

That habit makes dbt easier to reason about and keeps the project maintainable.
