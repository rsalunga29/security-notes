Insecure web server configurations cause the first type of HTTP Verb Tampering vulnerabilities. A web server's authentication configuration may be limited to specific HTTP methods, which would leave some HTTP methods accessible without authentication.

For example, the following Apache configuration is used to require authentication on a particular page:
```xml
<Directory "/var/www/html/admin">
    AuthType Basic
    AuthName "Admin Panel"
    AuthUserFile /etc/apache2/.htpasswd
    <Limit GET>
        Require valid-user
    </Limit>
</Directory>
```
If an attacker uses a HTTP method (e.g `PUT`), they will be able to bypass this authentication mechanism altogether.

Other example of misconfiguration on common web servers, including Tomcat and ASP.Net are as follows:
### Tomcat
```xml
<security-constraint>
    <web-resource-collection>
        <url-pattern>/admin/*</url-pattern>
        <http-method>GET</http-method>
    </web-resource-collection>
    <auth-constraint>
        <role-name>admin</role-name>
    </auth-constraint>
</security-constraint>
```
### ASP.Net
```xml
<system.web>
    <authorization>
        <allow verbs="GET" roles="admin">
            <deny verbs="GET" users="*">
        </deny>
        </allow>
    </authorization>
</system.web>
```