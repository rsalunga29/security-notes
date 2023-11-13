Also known as UNION-based SQL injection attack. This occurs when an attacker uses the `UNION` keyword to retrieve data from other tables within the database.

The `UNION` keyboard enables you to execute one or more additional `SELECT` queries and append the results to the original query. For example:
```sql
SELECT a, b FROM table1 UNION SELECT c, d FROM table2
```