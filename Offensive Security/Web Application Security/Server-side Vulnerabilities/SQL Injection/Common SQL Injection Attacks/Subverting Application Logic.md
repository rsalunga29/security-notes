Imagine an application that let's users login with a username and password, wherein the application checks the credentials provided by the user by performing a the following SQL query:
```sql
SELECT * FROM users WHERE username = 'admin' AND password = '12345678'
```
If the query returns the details of the user, then the login is successful. Otherwise, it is rejected.

In this case, an attacker can use the SQL comment sequence `--`