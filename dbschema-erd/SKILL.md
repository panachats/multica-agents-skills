---
name: dbschema-erd
description: Conventions for designing database schemas and producing ERDs for this workspace. Use this skill when modeling new tables, proposing schema changes, or drawing an entity-relationship diagram. Start by identifying the database engine from the project; then apply naming, key, data type, and ERD format conventions consistent with what the project already uses. Consult it before writing DDL so the design fits the existing schema.
---

# Database schema + ERD conventions

## Step 0 — discover the database engine

Check `.env`, `docker-compose.yml`, or the DB driver in `package.json` / `requirements.txt` to confirm the engine (PostgreSQL, MySQL, SQL Server, SQLite, etc.) before writing DDL. Engine affects data types, auto-increment syntax, and index creation.

## Design rules (engine-agnostic)

- **Primary keys:** every table has one. Prefer a surrogate auto-increment key unless a natural key is clearly stable.
  - PostgreSQL: `SERIAL` / `BIGSERIAL` or `GENERATED ALWAYS AS IDENTITY`
  - MySQL: `INT AUTO_INCREMENT`
  - SQL Server: `INT IDENTITY`
- **Foreign keys:** declare explicitly; name them `fk_<child>_<parent>`.
- **Naming:** consistent casing throughout — don't mix conventions within a table. Follow the convention already used in the project.
- **Data types:** choose the narrowest type that fits. For money/quantity use `DECIMAL(p,s)`, never `FLOAT`. For text that may contain non-ASCII characters, confirm the column encoding / collation.
- **Segments / codes:** if a table stores a business segment or category code, constrain it to the canonical set in `domain-context` via a lookup table or CHECK constraint.
- **Indexes:** add indexes to support actual query filters, especially date-range and segment filters. Keep columns sargable — see `sql-conventions`.
- **Audit columns:** add `created_at` / `updated_at` where traceability matters.

## ERD format — mermaid

Produce ERDs as mermaid `erDiagram` — renders in issues and docs, versions cleanly:

```
erDiagram
  ORDERS ||--o{ ORDER_ITEMS : contains
  ORDER_ITEMS {
    int     id PK
    int     order_id FK
    string  item_code
    decimal qty
    decimal unit_price
  }
  ORDERS {
    int     id PK
    string  segment_code
    date    order_date
  }
```

Include cardinality, mark `PK`/`FK`, keep field lists to what's relevant for the decision.

## Output

Deliver: mermaid ERD + `CREATE TABLE` DDL (in the project's engine syntax) + one-line rationale per design choice. Note any data migration needed and hand the DDL to `backend-dev`. Pair with the OpenAPI contract in `openapi-contract` — field names in API responses should align with the schema.
