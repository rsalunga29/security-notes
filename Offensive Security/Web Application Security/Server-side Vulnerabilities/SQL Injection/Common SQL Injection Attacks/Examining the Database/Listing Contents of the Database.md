Most database types, with exception of Oracle, have a set of views called information schema which provides information about the database.

For example, you can query `information_schema.tables` to list all the tables in the database:
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
## Listing Contents of an Oracle Database
LOLO