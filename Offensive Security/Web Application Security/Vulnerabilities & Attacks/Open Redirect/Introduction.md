An open redirect vulnerability occurs when an application allows a user to control a redirect or forward to another URL. If the app does not validate untrusted user input, all the attacker has to do is supply a URL that redirects an unsuspecting victim from a legitimate domain to an attacker-controlled site.

The following PHP code snippet shows an example :
```php
$red = $_GET['url'];
header("Location: " . $red);
```