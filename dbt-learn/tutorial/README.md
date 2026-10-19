# dbt Workspace Tutorial

This tutorial section is separate from the general project overview and is grounded in the current workspace structure of this repository.

## Suggested order

1. Start with [01-project-tour.md](/Users/arpanghosal/dbt/dbt-learn/tutorial/01-project-tour.md)
2. Continue to [02-model-flow.md](/Users/arpanghosal/dbt/dbt-learn/tutorial/02-model-flow.md)
3. Read [03-basic-dbtl-workflow.md](/Users/arpanghosal/dbt/dbt-learn/tutorial/03-basic-dbtl-workflow.md) to understand how dbt commands fit into the workflow
4. Use [04-where-to-edit-what.md](/Users/arpanghosal/dbt/dbt-learn/tutorial/04-where-to-edit-what.md) as a quick reference while working in this repo

## What this tutorial uses

The walkthrough is based on the current dbt project layout:

- Project configuration in [dbt_project.yml](/Users/arpanghosal/dbt/dbt-learn/dbt_project.yml)
- Staging models in [models/staging/](/Users/arpanghosal/dbt/dbt-learn/models/staging)
- Mart models in [models/marts/](/Users/arpanghosal/dbt/dbt-learn/models/marts)
- Tests in [tests/](/Users/arpanghosal/dbt/dbt-learn/tests)
- Seeds in [seeds/](/Users/arpanghosal/dbt/dbt-learn/seeds)
- Snapshots in [snapshots/](/Users/arpanghosal/dbt/dbt-learn/snapshots)
- Macros in [macros/](/Users/arpanghosal/dbt/dbt-learn/macros)

## Learning goal

By the end of this mini-tutorial, you should be able to:

- identify where sources, staging models, marts, tests, and docs live
- understand how the current models depend on each other
- use this repository as a practical dbt learning workspace
