Burp's scope rules use regular expressions in the host field, we can use the following to match all subdomains of the given domain.
```txt
.*\.domain\.com$
```
If the website has multiple domains, we just need to replace **.com** with **..***
```txt
.*\.domain\..*$
```