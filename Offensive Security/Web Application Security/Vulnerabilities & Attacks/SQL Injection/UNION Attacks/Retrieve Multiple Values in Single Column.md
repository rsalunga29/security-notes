In some cases, the query results may only be returned in a single column.

For situations like this, you can use string concatenation to retrieve multiple values together within a column column. For example, on Oracle you could submit the input:
```txt
' UNION SELECT username || '~' || password FROM users--
```
The double-pipe sequence (`||`) is a string concatenation operator in Oracle. The above will return a results containing usernames and passwords, like the following:
```txt
administrator~s3cure
wiener~peter
carlos~montoya
```
Different databases use different syntax to perform string concatenation. For more details, see the [SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet).