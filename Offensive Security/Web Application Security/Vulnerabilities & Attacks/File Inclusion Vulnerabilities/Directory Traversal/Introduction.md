Also known as path traversal, is a vulnerability that could potentially allow attackers to do any of the following:
- Read `/etc/passwd` and potentially find SSH Keys or know valid user names for a password spray attack
- Find other services on the box such as Tomcat and read the `tomcat-users.xml` file
- Discover valid PHP Session Cookies and perform session hijacking
- Read current web application configuration and source code

In some cases, an attacker might be able to write to arbitrary files, allowing them to modify application data or behavior, and ultimately take full control of the server.