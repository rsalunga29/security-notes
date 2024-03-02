## Querying the Database Type and Version
You can potentially identify both the database type and version by injecting provider-specific queries to see if one works. The following are some queries to determine the database version for some popular database types:

|Database type|Query|
|---|---|
|Microsoft, MySQL|`SELECT @@version`|
|Oracle|`SELECT * FROM v$version`|
|PostgreSQL|`SELECT version()`|

For example, you could use a `UNION` attack with the following input `' UNION SELECT @@version--`. Which might return the following output. In this case, you can confirm that the database is Microsoft SQL Server and see the version used:
```txt
Microsoft SQL Server 2016 (SP2) (KB4052908) - 13.0.5026.0 (X64)
Mar 18 2018 09:11:49
Copyright (c) Microsoft Corporation
Standard Edition (64-bit) on Windows Server 2016 Standard 10.0 <X64> (Build 14393: ) (Hypervisor
```
## Enumerating using Information Schema
The `information_schema` database contains metadata about the database, tables, and columns present on the server, making it a crucial step for attackers to view or enumerate when performing SQL injection vulnerabilities.

There are a couple of ways an attacker can use the `information_schema` database to fingerprint the database:
### Query `schemata` table to list all databases
