The Off-By-Slash vulnerability is caused by a missing trailing slash in the `location` instruction, which causes a Local File Inclusion vulnerability forcing the `alias` directive to return sensitive files. For example:
```nginx
server {
	listen 80 default_server;
	server_name _;

	location /static {
		alias /usr/share/nginx/static/;
	}

	location /api {
		proxy_pass http://apiserver/v1/;
	}
}
```

## Prevention
Add trailing slashes to all `location` instructions.