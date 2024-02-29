## GET Request
### Ffuf
```nix
ffuf -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -u http://get.target.com?FUZZ=key -ic
```
## POST Request
### Ffuf
```nix
ffuf -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -u http://post.target.com -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -ic
```
> Tip: In PHP, "POST" data "content-type" can only accept "application/x-www-form-urlencoded". So, we can set that in "ffuf" with `-H 'Content-Type: application/x-www-form-urlencoded'`.