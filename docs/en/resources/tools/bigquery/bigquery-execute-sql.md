---
title: "bigquery-execute-sql"
type: docs
weight: 1
description: >
  A "bigquery-execute-sql" tool executes a SQL statement against BigQuery.
aliases:
  - /resources/tools/bigquery-execute-sql
---

## About

A `bigquery-execute-sql` tool executes a SQL statement against BigQuery.
It's compatible with the following sources:

- [bigquery](../../sources/bigquery.md)

`bigquery-execute-sql` takes a required `sql` input parameter and runs the SQL
statement against the configured `source`. It also supports an optional `dry_run`
parameter to validate a query without executing it.

## Query Restriction

The `query_only` parameter allows you to restrict the tool to only execute SELECT queries, providing a read-only interface to your BigQuery data. When enabled:

- **Allowed**: SELECT statements that read data
- **Blocked**: CREATE, INSERT, UPDATE, DELETE, DROP, ALTER, and other data modification statements

This is useful for creating AI tools that can query and analyze data but cannot modify the database structure or contents.

## Example

```yaml
tools:
  execute_sql_tool:
    kind: bigquery-execute-sql
    source: my-bigquery-source
    description: Use this tool to execute sql statement.

  readonly_sql_tool:
    kind: bigquery-execute-sql
    source: my-bigquery-source
    description: Use this tool to execute SELECT queries only.
    query_only: true
```

## Reference

| **field**   | **type** | **required** | **description**                                                                                                                       |
| ----------- | :------: | :----------: | ------------------------------------------------------------------------------------------------------------------------------------- |
| kind        |  string  |     true     | Must be "bigquery-execute-sql".                                                                                                       |
| source      |  string  |     true     | Name of the source the SQL should execute on.                                                                                         |
| description |  string  |     true     | Description of the tool that is passed to the LLM.                                                                                    |
| query_only  | boolean  |    false     | When true, only allows SELECT statements. Other SQL types (CREATE, INSERT, UPDATE, DELETE, etc.) will be rejected. Defaults to false. |
