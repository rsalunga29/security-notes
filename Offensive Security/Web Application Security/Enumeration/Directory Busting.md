## Retrieve Common Directories
### GoBuster
```bash
gobuster dir -u http://target.com/ -w /usr/share/wordlists/dirb/common.txt -o results.txt
```
### Ffuf
```bash
ffuf -c -w /usr/share/wordlists/dirb/common.txt -u https://target.com/FUZZ -ic
```
## Retrieve Hidden Files
### GoBuster
```bash
gobuster dir -u http://target.com/ -w /usr/share/wordlists/dirb/common.txt -x .php,.txt,.html,.old,.bak,.zip,.rar -o results.txt
```
### Ffuf
```bash
ffuf -c -w /usr/share/wordlists/dirb/common.txt -u https://target.com/FUZZ -e .php,.txt,.html,.old,.bak,.zip,.rar -ic
```
## Web Extension Scanning
### Ffuf
```bash
ffuf -c -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt -u http://target.com/indexFUZZ -ic
```
## Recursive Scanning with Ffuf
```bash
ffuf -c -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt -u http://target.com/FUZZ -recursion -recursion-depth 1 -e .php -ic
```
## Exposed Git Folder
```bash
git-dumper http://vulnerable-website.com/.git
```