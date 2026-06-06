---
name: sql-conventions
description: SQL writing conventions for this workspace — index-safe filters, explicit aliasing, schema changes, and query structure. Use this skill whenever writing or refactoring SQL queries, stored procedures, views, CTEs, or schema changes. Start by identifying the database engine from the project (PostgreSQL, MySQL, SQL Server, SQLite, etc.) and apply the principles here using that engine's syntax. Consult it for any query work that filters large tables or mutates schema.
---

# SQL conventions

## Step 0 — discover the database engine

Before writing SQL, confirm what the project uses:

```shell
cat .env / docker-compose.yml / config/database.yml   # look for DB_URL, connection string
cat package.json / requirements.txt / *.csproj         # find the DB driver/ORM
```

Common signals: `pg` / `psycopg2` → PostgreSQL · `mysql2` / `mysqlclient` → MySQL · `mssql` / `System.Data.SqlClient` → SQL Server · `sqlite3` → SQLite. If unclear, ask before writing engine-specific syntax.

## Index-safe filtering

The most important rule across all engines: never wrap an indexed column in a function on the filter side — the engine can't seek the index.

**Bad — function kills the index:**
```sql
WHERE DATE_FORMAT(created_at, '%Y-%m') = '2026-06'   -- MySQL
WHERE TO_CHAR(created_at, 'YYYY-MM') = '2026-06'     -- PostgreSQL
WHERE CONVERT(VARCHAR(7), created_at, 111) = '2026/06' -- SQL Server
```

**Good — half-open range, column left bare (works on all engines):**
```sql
WHERE created_at >= '2026-06-01' AND created_at < '2026-07-01'
```

## CTE column aliasing

Alias every projected column explicitly in CTEs — documents intent, prevents column-mismatch errors on INSERT … SELECT, and makes downstream joins unambiguous.

```sql
WITH monthly_sales AS (
    SELECT
        item_id       AS item_id,
        SUM(qty)      AS total_qty,
        SUM(amount)   AS total_amount
    FROM orders
    GROUP BY item_id
)
SELECT * FROM monthly_sales;
```

## GROUP BY discipline

Every non-aggregated column in SELECT must appear in GROUP BY. Check the SELECT list against the GROUP BY clause before running.

## Schema changes

Prefer idempotent patterns over DROP + CREATE to avoid breaking dependents mid-deploy:

| Engine | Idempotent pattern |
|---|---|
| SQL Server | `CREATE OR ALTER PROCEDURE / VIEW` |
| PostgreSQL | `CREATE OR REPLACE FUNCTION / VIEW` |
| MySQL | `CREATE OR REPLACE VIEW` |

Before renaming an object, check what references it:
- **SQL Server:** `sys.dm_sql_referencing_entities` + `sys.sql_modules`
- **PostgreSQL:** `pg_depend` + `information_schema.view_column_usage`
- **MySQL:** `INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS`

## General

- Schema-qualify objects (`schema.table`) on all engines.
- Prefer set-based logic over loops/cursors.
- For domain tables and naming conventions, see `domain-context`.
