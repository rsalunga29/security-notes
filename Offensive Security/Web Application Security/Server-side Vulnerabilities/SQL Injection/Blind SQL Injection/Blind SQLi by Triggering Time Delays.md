Some applications are able to handle database errors gracefully, meaning there won't be any difference in the application's response when errors are induced. This means that [error-based SQL injection](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSQL%20Injection%2FBlind%20SQL%20Injection%2FError-based%20Blind%20SQLi%2FIntroduction) will not work.

In this situation, it is often possible to exploit the blind SQL injection vulnerability by trigger time delays depending on whether the injected condition is true or false. Normally, SQL queries are processed synchronously by the application, so a delay in execution of a SQL query also delays the application's response time. This technique allows an attacker to determine the truth of the injected condition based on the HTTP response time.

For example, using the following techniques on an application running Microsoft SQL server:
```txt
productId=1'||pg_sleep(10)
```

Additionally, We can also do conditional time delay, wherein we injected a condition and trigger a time delay if the condition is true:
```txt
productId=1' IF (1=2) WAITFOR DELAY '0:0:10'--
productId=1' IF (1=1) WAITFOR DELAY '0:0:10'--
```
- The first of these inputs does not trigger a delay, because the condition `1=2` is false.
- The second input triggers a delay of 10 seconds, because the condition `1=1` is true.

Using this technique, we can retrieve any data one character at a time by submitting like the following:
```txt
productId=1' IF (SELECT COUNT(Username) FROM Users WHERE Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') = 1 WAITFOR DELAY '0:0:{delay}'--
```