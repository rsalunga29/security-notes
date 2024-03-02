
## Enumerating Database using Information_Schema Database
The `information_schema` database contains metadata about the database, tables, and columns present on the server, making it a crucial step for attackers to view or enumerate when performing SQL injection vulnerabilities.

One way an attacker can use the `information_schema` database to enumerate the target application is to query the `schemata` table:
```sql
1' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- -
```
> Note: We are adding an extra dash (-) at the end, to show you that there is a space after (--).
