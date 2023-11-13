Consider an application that uses tracking cookies to gather analytics about usage. Requests to the application include a cookie header like this:
```txt
Cookie: TrackingId=u5YD3PapBcR4lN3e7Tj4
```
Which the application process and uses a SQL query to determine whether this is a known user:
```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = 'u5YD3PapBcR4lN3e7Tj4'
```
While this query is vulnerable to SQL Injection, the results are not returned to the user. However, the application does behave differently depending on whether the query returns any data. For example, submitting a recognized `TrackingId` will return a "Welcome back" message in the response.

This type of behavior is enough to be able to exploit blind SQL injection. You can retrieve information by triggering different responses depending on an injected condition.

Using the example above, suppose that the two following requests are sent in turn:
```txt
Cookie: TrackingId=u5YD3PapBcR4lN3e7Tj4' AND '1'='1
Cookie: TrackingId=u5YD3PapBcR4lN3e7Tj4' AND '1'='2
```
- The first of these values causes the query to return results, because the injected `AND '1'='1` condition is true. As a result, the "Welcome back" message is displayed.
- The second value causes the query to not return any results, because the injected condition is false. The "Welcome back" message is not displayed.

Another example, suppose you want to find out the password of a user called Administrator. You can do this by sending a series of inputs to test the password one character at a time.

You can start with the following input:
```txt
...xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'm
```
This returns the "Welcome back" message, indicating that the injected condition is true, and so the first character of the password is greater than `m`. 

Next send the following input:
```txt
...xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 't
```
This does not return the "Welcome back", indicating that the injected condition is false, and so the first character is not greater than `t`.

Eventually, the following input returns a "Welcome back" message, thereby confirming that the first character is `s`:
```txt
...xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) = 's
```