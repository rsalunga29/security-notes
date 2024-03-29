Information disclosure, also known as information leakage, is when a website unintentionally reveals sensitive information to its users. Depending on the context, websites may leak all kinds of information to a potential attacker, including:
- Data about other users, such as usernames or financial information
- Sensitive commercial or business data
- Technical details about the website and its infrastructure

Information disclosure arises in countless different ways, but can be categorized as follows:
- Failure to remove internal data from public content.
- Insecure configuration of the application and related technologies.
- Flawed design and behavior of the application.

The dangers of leaking sensitive information to users is fairly obvious, but disclosing technical details can be sometimes as serious. More often than not, sensitive information might be carelessly leaked to users who are simply browsing the application in a normal fashion. However, an attacker can force the application to reveal sensitive information by interacting with the application in unexpected or malicious ways (i.e Appending a tilde to a filename to retrieve an editor-generated backup file).

Some basic examples of information disclosure are as follows:
- Revealing the names of hidden directories, their structure, and their contents via a `robots.txt` file or directory listing
- Providing access to source code files via temporary backups
- Explicitly mentioning database table or column names in error messages
- Unnecessarily exposing highly sensitive information, such as credit card details
- Hard-coding API keys, IP addresses, database credentials, and so on in the source code
- Hinting at the existence or absence of resources, usernames, and so on via subtle differences in application behavior