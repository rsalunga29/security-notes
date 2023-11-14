Some applications are able to handle database errors gracefully, meaning there won't be any difference in the application's response when errors are induced. This means that [error-based SQL injection](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSQL%20Injection%2FBlind%20SQL%20Injection%2FError-based%20Blind%20SQLi%2FIntroduction) will not work.

In this situation, it is often possible to exploit the blind SQL injection vulnerability by trigger time delays depending on whether the injected condition is true or false. Normally, SQL queries are processed synchronously by the application, so a delay in execution of a SQL query also delays the application's response time. This technique allows an attacker to determine the truth of the injected condition based on the HTTP response time.

For example, using the following techniques on an application running Microsoft SQL server, we can test a condition and trigger a time delay if the condition is true:
```txt
...xyz'
```