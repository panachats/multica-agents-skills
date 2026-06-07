---
name: sql-injection-review
description: Security review focused on SQL injection risk in queries, application data-access code, and dynamic SQL. Use this skill when reviewing any change that builds or executes SQL, accepts user input that reaches a query, or constructs dynamic SQL. Consult it on every backend/data PR to flag string-concatenated queries and unparameterized input before merge.
---

# SQL injection review

Checklist for catching injection risk in this workspace's data layer. Post findings as PR comments with severity and a concrete fix; block merge on anything that lets untrusted input alter query structure.

## What to flag

1. **String-concatenated queries** — any query assembled by concatenating user/request input into the SQL string. This is the primary risk.

   **Unsafe:**
   ```sql
   SELECT * FROM orders WHERE channel = '" + channel + "'
   ```
   **Safe — parameterized:**
   ```sql
   SELECT * FROM orders WHERE channel = $1   -- bind channel as a parameter
   ```

2. **App-side concatenation** — query strings built in application code instead of using parameters or an ORM's parameter binding. Require parameterized queries everywhere user input reaches SQL.

3. **Dynamic SQL** — `EXEC`, prepared statements built from concatenated strings, or ORM `raw()` calls with interpolated input. Flag any pattern where untrusted input alters query structure.

4. **Identifiers from input** — table/column/sort-direction from input cannot be parameterized. Require an allow-list mapping (input → known-safe identifier), never direct interpolation.

5. **Dangerous sinks** — executing a concatenated query string, and any input forwarded to it.

## How to report

For each finding: severity (critical/high/medium/low), the exact line, why it's exploitable, and the parameterized fix. Critical/high block merge. If nothing is found, comment what you checked so the trail is clear.
