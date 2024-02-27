> Note: Proxying tools usually slows them down, therefore, only proxy tools when you need to investigate their requests, and not for normal usage.

## Proxychains
1. Edit `/etc/proxychains4.conf` and comment out the final line.
2. Add `http 127.0.0.1 8080` or your Burp Proxy settings at the end of the file.
3. Set Burp's Intercept to "on".
4. Add `proxychains` at the start of every command we want to intercept (i.e `proxychains curl http://10.10.10.10:8000`)
5. If using with Metasploit modules, make sure to run `set PROXIES http:127.0.0.1:8080` before executing any modules.