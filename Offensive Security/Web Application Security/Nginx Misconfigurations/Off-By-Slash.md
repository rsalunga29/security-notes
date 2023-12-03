The Off-By-Slash vulnerability is caused by a missing trailing slash in the `location` directive, making it possible to traverse one step up the path and cause a Local File Inclusion vulnerability forcing the `alias` directive to return sensitive files. For example:
```nginx
server {
	listen 80 default_server;
	server_name _;

	location /imgs {
		alias /usr/share/nginx/static/;
	}

	location /api {
		proxy_pass http://apiserver/v1/;
	}
}
```

## Prevention
Add trailing slashes to all `location` directives.