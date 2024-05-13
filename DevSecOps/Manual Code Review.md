Look for usage of known insecure functions.

Use `grep` to check the source code recursively. Example:
```bash
grep -r -n 'mysqli_query('
```