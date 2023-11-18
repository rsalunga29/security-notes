Imagine an application that let's users login with a username and password, wherein the application checks the credentials provided by the user by performing a the following SQL query:
```sql
SELECT * FROM users WHERE username = 'admin' AND password = '12345678'
```
If the query returns the details of the user, then the login is successful. Otherwise, it is rejected.

In this case, an attacker can use the SQL comment sequence `--` to remove the password check from the `WHERE` clause of the query, allowing the attacker to log in as any user without the need for a password. For example, submitting the username `administrator'--` and a blank password results in the following query:
```sql
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''
```
This query returns the user whose `username` is `administrator` and successfully logs the attacker in as that user.