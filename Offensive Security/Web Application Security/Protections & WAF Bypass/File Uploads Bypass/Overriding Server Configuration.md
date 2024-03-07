Servers won't typically execute files unless they have been configured to do so. For example, before an Apache server will execute PHP files requested by a client, the `/etc/apache2/apache2.conf` must have the following directives:
```txt
LoadModule php_module /usr/lib/apache2/modules/libphp.so
AddType application/x-httpd-php .php
```
Many servers allow developers to create a special configuration files within directories in order to override or add one or more global settings. Primary example for this is the usage of `.htaccess` - a directory-specific configuration file for Apache servers.

Similarly, IIS servers is also using a directory-specific configuration file called `web.config` which includes a directive that allows JSON files to be served to users:
```
<staticContent>
	<mimeMap fileExtension=".json" mimeType="application/json" />
</staticContent>
```
Web servers uses these configuration files when present, and users are typically not normally allowed to access them using HTTP requests. However, some servers occasionally fails to stop an attacker from uploading their own malicious configuration file.

Using Burp Proxy or Burp Repeater, we may have to replace the `Content-Type` to `text/plain` when uploading a malicious `.htaccess` or `web.config` file.