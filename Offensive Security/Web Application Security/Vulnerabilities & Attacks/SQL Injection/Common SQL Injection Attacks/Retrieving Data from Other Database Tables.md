In cases where the application responds with the results of a SQL query, often times, an attacker can use a SQL injection vulnerability to retrieve data from other tables within the database. You can use the `UNION` keyword to execute an additional `SELECT` query and append the results to the original query.

For example, if an application executes the following query containing the user input `Gifts`:
```sql
SELECT name, description FROM products WHERE category = 'Gifts'
```
An attacker can submit the input `' UNION SELECT username, password FROM users--`, result in a query:
```sql
SELECT name, description FROM products WHERE category = 'Gifts' UNION SELECT username, password FROM users--
```
This will cause the application to return all username and passwords along with the names and description of products.

This technique is also known as [UNION-based SQL injection](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSQL%20Injection%2FUNION%20Attacks%2FIntroduction).