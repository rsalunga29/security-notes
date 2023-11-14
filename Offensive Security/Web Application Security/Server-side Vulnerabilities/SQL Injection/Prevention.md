Most instances of SQL injection can be prevented by using parameterized queries, also known as "prepared statements".

For example, the following code is vulnerable to SQL injection because the user input is concatenated directly into the query:
```java
String query = "SELECT * FROM products WHERE category = '"+ input + "'";
Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery(query);
```
You can rewrite this code to use prepared statements to secure it against SQL injections:
```java
PreparedStatement statement = connection.prepareStatement("SELECT * FROM products WHERE category = ?");
statement.setString(1, input);
ResultSet resultSet = statement.executeQuery();
```

Parameterized queries must be used on any situations where untrusted input appears as data within the query, including the `WHERE` clause and values in an `INSERT` or `UPDATE` statement. However, for handling inputs such as table names or column names, including the `ORDER BY` clause, you need to use a different approach, such as:
- Whitelisting permitted input values.
- Using different logic to deliver the required behavior.

*Note: For a parameterized query to be effective in preventing SQL injection, the string that is used in the query must always be a hard-coded constant. It must never contain any variable data from any origin.*