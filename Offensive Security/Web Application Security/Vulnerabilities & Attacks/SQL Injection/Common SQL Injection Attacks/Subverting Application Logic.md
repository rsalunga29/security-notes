Imagine an application that let's users login with a username and password, wherein the application checks the credentials provided by the user by performing a the following SQL query:
```sql
SELECT * FROM users WHERE username = 'admin' AND password = '12345678'
```
If the query returns the details of the user, then the login is successful. Otherwise, it is rejected.
## Auth Bypass with Comments
In this case, an attacker can use the SQL comment sequence `-- ` to remove the password check from the `WHERE` clause of the query, allowing the attacker to log in as any user without the need for a password. For example, submitting the username `administrator'-- ` and a blank password results in the following query:
> Tip: Sometimes, there is no need to submit a username or any username. The following payload also works as well `' or '1'='1'-- `.

```sql
SELECT * FROM users WHERE username = 'administrator'-- ' AND password = ''
```
This query returns the user whose `username` is `administrator` and successfully logs the attacker in as that user.

> Note: In SQL, using two dashes only is not enough to start a comment. So, there has to be an empty space after them, so the comment starts with (`-- `), with a space at the end. This is sometimes URL encoded as (`--+`), as spaces in URLs are encoded as (`+`).
## Auth Bypass with OR operator
Consider the attacker plans to bypass the authentication logic in an admin panel using SQL injection, but without knowing the admin's username, the query will still return `false` and prevents the attacker from logging in.

However, for an attacker to successfully login, all they have to do is to force an "overall true" query. Which can be achieved by injecting an `OR` condition into the password field:
```
Username field: notAdmin' OR '1' = '1'
Password field: something' OR '1' = '1
```
Which in turn will execute the following query:
```sql
SELECT * FROM logins WHERE username = 'notAdmin' OR '1' = '1' AND password = 'something' OR '1' = '1';
```