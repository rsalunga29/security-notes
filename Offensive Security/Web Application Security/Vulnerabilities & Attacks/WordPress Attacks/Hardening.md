Below are some best practices for preventing attacks against a WordPress site.
## Perform Regular Updates
This is a key principle for any application or system and can greatly reduce the risk of a successful attack. Make sure that WordPress core, as well as all installed plugins and themes, are kept up-to-date. We can also modify the `wp-config.php` file to enable automatic updates by inserting the following lines:
```php
define( 'WP_AUTO_UPDATE_CORE', true );
add_filter( 'auto_update_plugin', '__return_true' );
add_filter( 'auto_update_theme', '__return_true' );
```
## Plugin and Theme Management
Only installed trusted themes and plugins from the WordPress.org website. Before installing a plugin or theme, check its reviews, popularity, number of installs, and last update date. If either has not been updated in years, it could be a sign that it is no longer maintained and may suffer from unpatched vulnerabilities. Routinely audit your WordPress site and remove any unused themes and plugins. This will help to ensure that no outdated plugins are left forgotten and potentially vulnerable.
## Install Security Plugins
Some plugins can be used to enhance the security of your WordPress instance. These plugins can be used as a web application firewall (WAF), malware scanner, activity monitoring and auditing, brute force attack prevention, etc.

Below are some of the most popular WordPress security plugins:
- [Sucuri Security](https://wordpress.org/plugins/sucuri-scanner/)
	- Security Activity Monitoring
	- File Integrity Monitoring
	- Remote Malware Scanning
	- Blacklist Monitoring
- [iThemes Security](https://wordpress.org/plugins/better-wp-security/)
	- Two-Factor Authentication (2FA)
	- WordPress Salts & Security Keys
	- Google reCAPTCHA
	- User Action Logging
- [Wordfence Security](https://wordpress.org/plugins/wordfence/)
	- Web Application Firewall (WAF)
	- Real-time firewall rule and malware signature updates (premium)
	- Real-time blacklisting of known malicious IP addresses (premium)
## User Management
The following user-related best practices will help improve the overall security of a WordPress site.
- Disable the standard `admin` user and create accounts with difficult to guess usernames
- Enforce strong passwords
- Enable and enforce two-factor authentication (2FA) for all users
- Restrict users' access based on the concept of least privilege
- Periodically audit user rights and access. Remove any unused accounts or revoke access that is no longer needed
## Configuration Management
Certain configuration changes can increase the overall security posture of a WordPress installation.
- Install a plugin that disallows user enumeration so an attacker cannot gather valid usernames to be used in a password spraying attack
- Limit login attempts to prevent password brute-forcing attacks
- Rename the `wp-admin.php` login page or relocate it to make it either not accessible to the internet or only accessible by certain IP addresses