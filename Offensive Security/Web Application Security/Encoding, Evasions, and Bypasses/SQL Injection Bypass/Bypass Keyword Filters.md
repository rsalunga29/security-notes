The first limitation that we may encounter when dealing with filters are restrictions on keywords.
## Case Changing
The simplest and weakest filters are the ones that perform case sensitive checks (i.e filter blocks all the `SELECT` and `select` keywords).

This can easily be bypassed by changing the cases of each character:
```sql
SeLeCt ...
SELeCT ...
```
### Using Intermediary Characters
Sometimes filters uses spaces to delimit a specific keyword. Depending on the DBMS version, a we can use both comments or other characters:
```sql
SELECT/**/values/**/and/**/.../**/or/**/
SELECT[sp]values[sp]and...[sp]or[sp]
```

We can also use other altnernatives:
```sql
SELECT"values"from'table'where/**/1
SELECT(values)from(table)where(1)
SELECT"values"''from'table'where(1)
SELECT+"values"%A0from'table'
```
## Circumventing Encoding
Encoding is another handy trick we can leverage in our arsenal. It all depends on how the application processes data.

Usually when the requests are sent through the internet via HTTP, they are URL encoded. If the filter doesn't decode the request, we can bypass this by sending a URL-encoded character or string.

We can also use **Double URL Encoding**, which URL encodes an already URL-encoded string. If the filter only decodes the request once, it will not find anything malicious. Then when the application receives the request, it will decode the contents and trigger the malicious request.
## Replaced Keywords
When regex's are tricky, we have to find alternative methods to bypass them. Replacing blocked keywords is one of these methods.

In MySQL and MSSQL, the `&&` and `||` can be replaced by `AND` and `OR`, and vice versa. If both are blocked, then we must use `UNION`.

If `UNION` is filtered, the following alternatives can be used:
```sql
... UNION(SELECT 'VALUES'...) && ...
... UNION ALL SELECT ...
... UNION DISTINCT SELECT ...
... /*!00000 UNION*//*!00000 SELECT*/ ...
```
If none of the above works, we must switch to attempting [blind SQLi](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FVulnerabilities%20%26%20Attacks%2FSQL%20Injection%2FBlind%20SQL%20Injection%2FIntroduction) instead.

In Oracle, we can use `INTERSECT` or `MINUS` operators.

If the filter blocks the `WHERE` keyword, we can use `GROUP BY` and `HAVING` as alternatives. For example:
```sql
SELECT id FROM users GROUP BY id HAVING id=5...
```

If `GROUP BY` is blocked, we must switch to attempting [blind SQLi](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FVulnerabilities%20%26%20Attacks%2FSQL%20Injection%2FBlind%20SQL%20Injection%2FIntroduction) instead.

If `HAVING` is filtered, in this case we must leverage functions like `GROUP_CONCAT`, functions that manipulates strings, etc. (blind SQLi)

If `SELECT` is filtered, it's an *authentic tragedy*. The exploitation can vary and really depends upon the injection point. Alternatively, you can use functions that manipulates files, such as `load_files` (MySQL).

Another option, brute-force or guess the column names by appending other `WHERE` condition.

Another option, is being able to invoke the stored `procedure analyse()`, which returns "juicy" information about the query that was just executed. For example:
```sql
SELECT * FROM employees procedure analyse()
```
