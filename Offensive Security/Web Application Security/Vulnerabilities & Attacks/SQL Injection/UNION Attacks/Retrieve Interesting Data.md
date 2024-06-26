Once you have determined the number of columns and which columns can hold string data, you are already in position to retrieve interesting data. For example, we can now retrieve user credentials, so long as we meet the following requirements:
- The original query returns two columns, both of which can hold string data.
- The injection point is a quoted string within the `WHERE` clause.
- The database contains a table called `users` with the columns `username` and `password`.

You can submit the following input to retrieve the contents of `users` table:
```txt
' UNION SELECT username, password FROM users--
```

In order to perform the example attack, you need to know that a table named `users` exists with two columns called `username` and `password`. Without this information, you would have to guess the names of the tables and columns. All modern databases provide ways to [examine the database structure](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSQL%20Injection%2FCommon%20SQL%20Injection%20Attacks%2FEnumerating%20the%20Database), and determine what tables and columns they contain.