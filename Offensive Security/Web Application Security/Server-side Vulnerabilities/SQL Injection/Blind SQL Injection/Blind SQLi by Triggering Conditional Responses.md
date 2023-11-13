Consider an application that uses tracking cookies to gather analytics about usage. Requests to the application include a cookie header like this:
```txt
Cookie: TrackingId=u5YD3PapBcR4lN3e7Tj4
```
When a request containing a `TrackingId` cookie is processed, the application uses a SQL query to determine whether this is a known user:
```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = 'u5YD3PapBcR4lN3e7Tj4'
```
While this query is vulnerable to SQL Injection, the results are not returned to the user. However, the application does behave differently depending on whether the query returns any data. For example, submitting a recognized `TrackingId` will return a "Welcome back" message in the response.

This type of behavior is enough to be able to exploit blind SQL injection. You can retrieve information by triggering different responses depending on an injected condition.

Using the example above, suppose that the two followin