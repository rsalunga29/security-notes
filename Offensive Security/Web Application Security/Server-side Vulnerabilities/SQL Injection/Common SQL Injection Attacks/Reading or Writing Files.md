In addition to gathering data from various tables and databases within the DBMS, a SQL Injection can also be leveraged to perform many other operations, such as reading and writing files on the server and even gaining remote code execution on the back-end server.
## Prerequisites
Reading data is much more common than writing data, which is strictly reserved for privileged users in modern DBMSes, as it can lead to system exploitation.

For MySQL, the DB user must have the `FILE` privilege to load a file's content into a table and then dump data from that table and read files. Additionally, the global MySQL variable `secure_file_priv` must be disabled for a DB user to be able to upload file into a directory they have a write-access to.
## Read File
The `LOAD_FILE()` function can be used in MariaDB / MySQL to read data from files. The function takes in just one argument, which is the file name. In order to read the contents of `/etc/passwd`, we can use the following query:
```sql
SELECT LOAD_FILE('/etc/passwd');
```
## Write File
First, we have to check if the global variable `secure_file_priv` is disabled using the following query. If the result returns empty, that means we can write files to any location.
```sql
SELECT variable_name, variable_value FROM information_schema.global_variables where variable_name="secure_file_priv";
```

The `SELECT INTO OUTFILE` statement can be used to write data from select queries into files. This is usually used for exporting data from tables. For example, the following query will output the results into the `/tmp/credentials` file:
```sql
SELECT * from users INTO OUTFILE '/tmp/credentials';
```