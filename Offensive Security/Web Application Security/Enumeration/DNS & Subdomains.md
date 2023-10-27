## GoBuster
### DNS
```nix
gobuster dns -d target.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
### VHosts
```nix
gobuster vhosts –u target.com –w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
## Sublist3r
```nix
python3 sublist3r.py -d target.com -b -p 80,443,21 -v
```
## Ffuf
```nix
ffuf -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://target.com -H "Host: FUZZ.target.com" -fw 5338
```
### Wfuzz
```nix
wfuzz -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://target.com/ -H "HOST: FUZZ.target.com" --hw 28
```
### Subfinder
```nix
subfinder -d target.com
```
### OWASP Amass
```nix
amass enum -passive -d target.com -src
```