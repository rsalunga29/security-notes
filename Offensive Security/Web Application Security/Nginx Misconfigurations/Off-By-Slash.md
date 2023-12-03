The Off-By-Slash vulnerability is caused by a missing trailing slash in the `location` directive combined with the `alias` directive, making it possible to traverse one step up the path and cause a [Local File Inclusion](obsidian://open?vault=Security%20Notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FIntroduction) vulnerability. For example:
```nginx
server {
	listen 80 default_server;
	server_name _;

	location /assets {
		alias /var/www/html/assets/;
	}
}
```
An attacker can submit a request like the following to read sensitive files such as environment file or git file:
```txt
https://vulnerable-website.com/assets../.env
```
```txt
https://vulnerable-website.com/assets../.git/HEAD
```
The payloads above will cause the `alias` directive to transform to:
```
/var/www/html/assets/../.env
```

This vulnerability also applies to other commands such as `proxy_pass`. For example:
```nginx
server {
	listen 80 default_server;
	server_name _;

	location /api {
		proxy_pass http://apiserver/v1/;
	}
}
```
## Prevention
Add trailing slashes to all `location` directives.