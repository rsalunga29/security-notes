The following is the directory structure of a default WordPress install, showing key files and subdirectories necessary for the website to function properly.
```
├── index.php
├── license.txt
├── readme.html
├── wp-activate.php
├── wp-admin
├── wp-blog-header.php
├── wp-comments-post.php
├── wp-config.php
├── wp-config-sample.php
├── wp-content
├── wp-cron.php
├── wp-includes
├── wp-links-opml.php
├── wp-load.php
├── wp-login.php
├── wp-mail.php
├── wp-settings.php
├── wp-signup.php
├── wp-trackback.php
└── xmlrpc.php
```
## Key WordPress Files and Directories
The root directory contains files that are needed to configure WordPress to function properly, these are:
- `index.php` is the homepage of WordPress.
- `license.txt` contains useful information such as the version of WordPress installed.
- `wp-activate.php` is used for the email activation process when setting up a new WordPress website.
- `xmlrpc.php` is a file representing a feature of WordPress that enables data to be transmitted with HTTP acting as the transport mechanism and XML as the encoding mechanism. This can be replaced by the WordPress [REST API](https://developer.wordpress.org/rest-api/reference).
- `wp-admin` is a folder that contains the login page for administrator access and backend dashboard. The login page can be located in any of these following paths (This file can also be renamed to make it more challenging to find the login page):
	- `/wp-admin/login.php`
	- `/wp-admin/wp-login.php`
	- `/login.php`
	- `/wp-login.php`
- `wp-config.php` contains information required by WordPress to connect to the database. This file can also be used to activate `DEBUG` mode, which can be useful in troubleshooting.
- `wp-content` folder is the main directory where plugins and themes are stored. There is also a subdirectory named `uploads/` wh