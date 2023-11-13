Some applications carry out SQL queries but their behavior doesn't change. This means that [injecting different boolean conditions ](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSQL%20Injection%2FBlind%20SQL%20Injection%2FBlind%20SQLi%20by%20Triggering%20Conditional%20Responses)makes no difference to the application's response.

In this case, another method to use is to induce the application to return an error message when a SQL error occurs. You can modify the query so that it causes a database error only if the condition is true. For example:
```txt
...xyz' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 'a' END)='a
...xyz' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a
```
These inputs use the `CASE` keyword to test a condition and return a different expression depending on whether the expression is true:
- With the first input, the `CASE` expression evaluates to `'a'`, which does not cause any error.
- With the second input, it evaluates to `1/0`, which causes a divide-by-zero error.

Using this technique, you can retrieve data by testing one character at a time:
```txt
...xyz' AND (SELECT CASE WHEN (Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') THEN 1/0 ELSE 'a' END FROM Users)='a
```

This follow the same technique and process as "[triggering a conditional response](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSQL%20Injection%2FBlind%20SQL%20Injection%2FBlind%20SQLi%20by%20Triggering%20Conditional%20Responses)" except that we are inducing an error response instead of a boolean condition.
## Example from PortSwigger Web Academy
The video below uses the Cluster Bomb attack type

[![SQL Injection - Lab #12 - Blind SQL injection with conditional errors ](https://img.youtube.com/vi/_7w-KEP_K5w/0.jpg)](https://www.youtube.com/watch?v=_7w-KEP_K5w)

The video below uses the Sniper attack type and manual brute forcing

[![Blind SQL injection with conditional errors (Video solution, Audio) )](https://img.youtube.com/vi/HbaD3maRucc/0.jpg)](https://www.youtube.com/watch?v=HbaD3maRucc)