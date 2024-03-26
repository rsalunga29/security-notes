Also known as UNION-based SQL injection attack. This occurs when an attacker uses the `UNION` keyword to retrieve data from other tables within the database.

The `UNION` keyboard enables you to execute one or more additional `SELECT` queries and append the results to the original query. For example:
```sql
SELECT a, b FROM table1 UNION SELECT c, d FROM table2
```
The query above will return a single result set with two columns, containing values from columns `a` and `b` in `table` and columns `c` and `d` in `table2`.

For a `UNION` query to work, two key requirements must be met:
- The individual queries must return the same number of columns.
- The data types in each column must be compatible between the individual queries.

For a UNION-based SQL injection attack to work, make sure you attack meets these two requirements. This normally involves finding out:
- How many columns are being returned from the original query.
- Which columns returned from the original query are of a suitable data type to hold the results from the injected query.