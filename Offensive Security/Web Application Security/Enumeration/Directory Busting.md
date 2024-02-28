## Retrieve Common Directories
### GoBuster
```nix
gobuster dir -u http://target.com/ -w /usr/share/wordlists/dirb/common.txt -o results.txt
```
### Ffuf
```nix
ffuf -c -w /usr/share/wordlists/dirb/common.txt -u https://target.com/FUZZ -ic
```
## Retrieve Hidden Files
### GoBuster
```nix
gobuster dir -u http://target.com/ -w /usr/share/wordlists/dirb/common.txt -x .php,.txt,.html,.old,.bak,.zip,.rar -o results.txt
```
### Ffuf
```nix
ffuf -c -w /usr/share/wordlists/dirb/common.txt -u https://target.com/FUZZ -e .php,.txt,.html,.old,.bak,.zip,.rar -ic
```
## Recursive Scanning with Ffuf
```nix
ffuf -c -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt -u http://target.com/FUZZ -recursion -recursion-depth 1 -e .php -ic
```
## Exposed Git Folder
```nix
git-dumper http://vulnerable-website.com/.git
```