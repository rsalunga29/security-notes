An essential part of any enumeration phase is knowing the version number of the application we are targeting. We can do this manually by using browser developer tools or CLI utilities, alternatively, we can also use [WPScan](https://github.com/wpscanteam/wpscan) to automate this step.
## Core Version
The first and easiest step is reviewing the page source code, which can be done by using the browser developer tools.

In WordPress, the versions are shown in following HTML tags:
**Meta Tags**
```html
...SNIP...
<meta name="generator" content="WordPress 5.3.3" />
...SNIP...
```
**CSS Link Tags**
```html
...SNIP...
<link rel='stylesheet' id='bootstrap-css'  href='http://blog.inlanefreight.com/wp-content/themes/ben_theme/css/bootstrap.css?ver=5.3.3' type='text/css' media='all' />
<link rel='stylesheet' id='transportex-style-css'  href='http://blog.inlanefreight.com/wp-content/themes/ben_theme/style.css?ver=5.3.3' type='text/css' media='all' />
<link rel='stylesheet' id='transportex_color-css'  href='http://blog.inlanefreight.com/wp-content/themes/ben_theme/css/colors/default.css?ver=5.3.3' type='text/css' media='all' />
<link rel='stylesheet' id='smartmenus-css'  href='http://blog.inlanefreight.com/wp-content/themes/ben_theme/css/jquery.smartmenus.bootstrap.css?ver=5.3.3' type='text/css' media='all' />
...SNIP...
```
**JavaScript Tags**
```html
<script type='text/javascript' src='http://blog.inlanefreight.com/wp-includes/js/jquery/jquery.js?ver=1.12.4-wp'></script>
<script type='text/javascript' src='http://blog.inlanefreight.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=1.4.1'></script>
<script type='text/javascript' src='http://blog.inlanefreight.com/wp-content/plugins/mail-masta/lib/subscriber.js?ver=5.3.3'></script>
<script type='text/javascript' src='http://blog.inlanefreight.com/wp-content/plugins/mail-masta/lib/jquery.validationEngine-en.js?ver=5.3.3'></script>
<script type='text/javascript' src='http://blog.inlanefreight.com/wp-content/plugins/mail-masta/lib/jquery.validationEngine.js?ver=5.3.3'></script>
```
## Plugins and Themes Version
We can also find information about the installed plugins by reviewing the source code manually or filtering for information using `curl` and other CLI utitlities.
**Plugins**
```bash
curl -s -X GET http://target-website.com | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'wp-content/plugins/*' | cut -d"'" -f2
```
**Themes**
```bash
curl -s -X GET http://target-website.com | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'themes' | cut -d"'" -f2
```

The response headers may also contain version numbers for specific plugins.

However, not all installed plugins and themes can be discovered passively. In this case, we have to send requests to the server actively to enumerate them. For example:
```bash
curl -I -X GET http://target-website.com/wp-content/plugins/mail-masta/
```
If the content does not exist, we will receive a `404 Not Found error`. The same applied to installed themes.

>Note: Even if a plugin or theme is deactivated, it may still be accessible, and therefore we can gain access to its associated scripts and functions.
## Site Users
Enumerating a list of valid users is a critical phase of a WordPress security assessment. Armed with this list, we may be able to guess default credentials or perform a brute force password attack.
### First Method
The first method is reviewing posts to uncover the ID assigned to the user and their corresponding username. If we mouse over any post's author linked titled "by user", a link to the user's account will appear in the browser's left/right corner.

Alternatively, we can use the following `curl` command to enumerate via user id. The admin user is usually assigned the user id `1`:
```bash
curl -s -I -X GET http://target-website.com/?author=1
```
If the user does not exist, we receive a `404 Not Found error`, otherwise it will redirect us to the user's profile page or the login page.
### Second Method
The second method requires interaction with the `JSON` endpoint, which allows us to obtain a list of users. This was changed in WordPress core after version 4.7.1, and later versions only show whether a user is configured or not. Before this release, all users who had published a post were shown by default.
```bash
curl http://target-website.com/wp-json/wp/v2/users | jq
```
## Uploaded Files
Make sure to check if `wp-content` is accessible and directory fuzzing can be performed.
