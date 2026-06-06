---
name: sql-injection-review
description: Security review focused on SQL injection risk in T-SQL, application data-access code, and linked-server or OPENQUERY calls. Use this skill when reviewing any change that builds or executes SQL, accepts user input that reaches a query, or constructs dynamic SQL. Consult it on every backend/data PR to flag string-concatenated queries, unparameterized input, and unsafe OPENQUERY string-building before merge.
---

# SQL injection review

Checklist for catching injection risk in this workspace's data layer. Post findings as PR comments with severity and a concrete fix; block merge on anything that lets untrusted input alter query structure.

## What to flag

1. **String-concatenated queries** — any query assembled with `+` from variables that include user/request input. This is the primary risk.

   **Unsafe:**
   ```sql
   SET @sql = 'SELECT * FROM Orders WHERE Channel = ''' + @channel + '''';
   EXEC(@sql);
   ```
   **Safe — parameterized via sp_executesql:**
   ```sql
   EXEC sp_executesql
        N'SELECT * FROM Orders WHERE Channel = @channel',
        N'@channel NVARCHAR(20)', @channel = @channel;
   ```

2. **App-side concatenation** — query strings built in application code instead of using parameters / an ORM's parameter binding. Require parameterized queries everywhere user input reaches SQL.

3. **Unsafe OPENQUERY building** — `OPENQUERY` takes a literal string, so dynamic OPENQUERY is easy to get wrong. If any part of the inner query comes from input, it must be validated/escaped or, better, the value should be filtered locally after a parameterized pull. Flag any OPENQUERY whose inner SQL is concatenated from variables.

4. **Identifiers from input** — table/column/sort-direction coming from input can't be parameterized. Require an allow-list mapping (input → known-safe identifier), never direct interpolation.

5. **Dangerous sinks** — direct `EXEC(@sql)` on a concatenated string, and any input forwarded to it.

## How to report

For each finding: severity (critical/high/medium/low), the exact line, why it's exploitable, and the parameterized fix. Critical/high block merge. If nothing is found, comment what you checked so the trail is clear.

For T-SQL style and the linked-server patterns being reviewed, see `sqlserver-tsql` and `dynamics-ax-integration`.
