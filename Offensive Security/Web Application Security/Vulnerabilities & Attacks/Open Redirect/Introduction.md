An open redirect vulnerability occurs when an application allows a user to control a redirect or forward to another URL. If the app does not validate untrusted user input, all the attacker has to do is supply a URL that redirects an unsuspecting victim from a legitimate domain to an attacker-controlled site.

The following PHP code snippet is an example of a redirection functionality:
```php
$red = $_GET['url'];
header("Location: " . $red);
```

The code above sets the value of `$red` without any validation, this could lead to an open redirect vulnerability. The malicious URL an attacker would send leveraging the Open Redirect vulnerability would look as follows:
```txt
http://trusted.site/index.php?url=https://evil.com
```

During an engagement, it is wise to look for the following URL parameters which is commonly used for redirections (you'll often see them in login pages):
- `?url=`
- `?link=`
- `?redirect=`
- `?redirecturl=`
- `?redirect_uri=`
- `?return=`
- `?return_to=`
- `?returnurl=`
- `?go=`
- `?goto=`
- `?exit=`
- `?exitpage=`
- `?fromurl=`
- `?fromuri=`
- `?redirect_to=`
- `?next=`
- `?newurl=`
- `?redir=`