## Retrieve Common Directories
### GoBuster
```nix
gobuster dir -u http://target.com/ -w /usr/share/wordlists/dirb/common.txt -o results.txt
```
### Ffuf
```nix
gobuster dir -u http://target.com/ -w /usr/share/wordlists/dirb/common.txt -x .php,.txt,.html,.old,.bak,.zip,.rar -o results.txt
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