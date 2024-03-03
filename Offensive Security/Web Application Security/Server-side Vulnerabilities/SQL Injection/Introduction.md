Also known as SQLi, is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. This can allow an attacker to view sensitive data, including data of other users or any other data that the application can access. In many cases, an attacker can modify or delete this data, causing persistent changes to the application's content or behavior.

In some situations, an attacker can escalate a SQL injection attack to compromise the underlying backend infrastructure or perform a denial-of-service attack.

A successful SQL injection attack can result in unauthorized access to sensitive data, such as:
- Passwords
- Personal user information
- Credit card details

This kind of attack has been used in many high-profile data breaches over the years, which has caused reputational damage and regulatory fines. In severe cases, SQL injection was used to obtain a persistent backdoor into an organization's system, leading to a long-term compromise for an extended period of time.
## Detecting SQL Injection
You can detect a SQL injection manually using a set of tests against every entry point in the application:
- The following characters and look for errors or other anomalies:
	- Single-quote `'` or `%27` as URL-encoded
	- Double-quote `"` or `%22` as URL-encoded
	- Hashtag `#` or `%23` as URL-encoded
	- Semicolon `;` or `%3B` as URL-encoded
	- Ending parenthesis `)` or `%29` as URL-encoded
- Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and look for systematic differences in the application responses.
- Boolean conditions such as `OR 1=1` and `OR 1=2`, and look for differences in the application's responses.
- Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
- [OAST](https://portswigger.net/burp/application-security-testing/oast) payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions.

Alternatively, you can use tools such as [Burp Scanner](https://portswigger.net/burp/vulnerability-scanner) or [sqlmap](https://github.com/sqlmapproject/sqlmap).
## Cheat Sheet
This [cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) contains some examples of useful syntax that you can use to perform a variety of tasks that often arises when performing SQL injection attacks.

There will be times where the `SELECT` keyword won't work.
## Usage of sqlmap
To automate detection and exploitation of SQL injection vulnerabilities, the [sqlmap](https://github.com/sqlmapproject/sqlmap) tool can be used.
```nix
sqlmap -u "http://target.com/products.php?id=1" --batch --dump
```
### SQLmap Levels and Risk
The `--level` and `--risk` options are critical to understand when using sqlmap, because they decide what tests are performed and what payloads are used when looking for SQL injections in web applications. They can make the difference between finding and not finding SQL injection vulnerabilities.

| Level | Description                                                                                                                                                                          |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1     | Tests all `GET` and `POST` parameters. Default level.                                                                                                                                |
| 2     | Tests for HTTP Cookie headers. Set `--cookie` parameter manually to test specific cookies. Use `--param-exclude` parameter to skip specific cookies. (Addtl parameters are optional) |
| 3     | Tests for HTTP User-Agent and Referer headers.                                                                                                                                       |
| 4     | Enables more payloads such as boolean-based blind, etc...                                                                                                                            |
| 5     | Tests for HTTP Host headers and other additional checks.                                                                                                                             |
> Note: Higher levels includes tests from their lower levels. If level is set to 3, sqlmap will include levels 1 and 2 test cases. Additionally, the higher the level, the higher number of requests the tool makes.

| Risk | Description     |
| ---- | --------------- |
| 1    | Least offensive |
| 2    |                 |
| 3    |                 |
> Note: The higher the risk level, the more dangerous the payloads are, which can lead to unintentional modification of data or take down the database itself.