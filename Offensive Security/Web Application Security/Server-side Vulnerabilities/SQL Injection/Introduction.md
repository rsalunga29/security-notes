Also known as SQLi, is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. This can allow an attacker to view sensitive data, including data of other users or any other data that the application can access. In many cases, an attacker can modify or delete this data, causing persistent changes to the application's content or behavior.

In some situations, an attacker can escalate a SQL injection attack to compromise the underlying backend infrastructure or perform a denial-of-service attack.

A successful SQL injection attack can result in unauthorized access to sensitive data, such as:
- Passwords
- Personal user information
- Credit card details

This kind of attack has been used in many high-profile data breaches over the years, which has caused reputational damage and regulatory fines. In severe cases, SQL injection was used to obtain a persistent backdoor into an organization's system, leading to a long-term compromise for an extended period of time.
## Detecting SQL Injection
You can detect a SQL injection manually using a set of tests against every entry point in the application:
- The single quote character `'` and look for errors or other anomalies.
- Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and look for systematic differences in the application responses.
- Boolean conditions such as `OR 1=1` and `OR 1=2`, and look for differences in the application's responses.
- Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
- [OAST](https://portswigger.net/burp/application-security-testing/oast) payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions.

Alternatively, you can use tools such as [Burp Scanner](https://portswigger.net/burp/vulnerability-scanner) or [sqlmap](https://github.com/sqlmapproject/sqlmap).
## Cheat Sheet
This [cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) contains some examples of useful syntax that you can use to perform a variety of tasks that often arises when performing SQL injection attacks.