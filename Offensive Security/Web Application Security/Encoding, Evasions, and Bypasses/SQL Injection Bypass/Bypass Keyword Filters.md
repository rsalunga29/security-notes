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

In MySQL and MSSQL, the `&&` and `||` can be replaced by `AND` and `OR`, and vice vers