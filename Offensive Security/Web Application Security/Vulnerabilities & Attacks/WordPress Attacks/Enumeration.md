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