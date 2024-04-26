## Subdomain Enumeration
### Passive & Active Enumeration
```bash
subfinder -d domain.com -o subfinder.txt
```
### Enumeration via Certificate Transparency Logs
```bash
assetfinder --subs-only domain.com >> assetfinder.txt
```
### LLL
### Generate subdomain patterns based on existing subdomains
```bash
subfinder -d domain.com | alterx | dnsx
```