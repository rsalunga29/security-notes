When you perform a UNION-based SQL injection attack, you need to determine how many columns are being returned from the original query. There are two effective methods to do this.
## ORDER BY Method
The first method involves injecting a series of `ORDER BY` clauses and incrementing the specific column index until an error occurs. For example:
```txt
' ORDER BY 1--
' ORDER BY 2--
etc...
```
This series of payloads modifies the original query to order the results by different columns in the result set. The column in an `ORDER BY` clause can be specified by its index. When the specified index exceed the number of the actual columns in the results, the database returns an error:
```txt
The ORDER BY position number 3 is out of range of the number of items in the select list.
```
However, some applications will only return a generic error response or will not return any response at all. Regardless, as long as you can detect some difference in the response, you can guess how many columns are being returned from the query.
## UNION SELECT Method
The second method involves submitting a series of `UNION SELECT` payloads specifying a different number of `null` values, for example:
```txt
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
etc...
```
If the number of nulls does not match the number of columns, the database returns an error:
```txt
All queries combined using a UNION, INTERSECT or EXCEPT operator must have an equal number of expressions in their target lists.
```
Since data types in each columns must be compatible between the original and injected values, we use `NULL` as it is convertible to every common data type, increasing the chances that the payload will succeed when the column count is correct.