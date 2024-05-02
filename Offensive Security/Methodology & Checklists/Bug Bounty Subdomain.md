## Passive & Active Enumeration
```bash
subfinder -d domain.com -o subfinder.txt
```
## Enumeration via Certificate Transparency Logs
```bash
assetfinder --subs-only domain.com >> assetfinder.txt
```
## Enumeration via ASN Mapping
```bash
asnmap -d domain.com | dnsx -silent -resp-only -ptr > asnmapping.txt
```
## Generate subdomain patterns based on existing subdomains
```bash
subfinder -d domain.com | alterx | dnsx
```
## Dynamic enumeration with alterx
```bash
echo domain.com | alterx -enrich | dnsx > alterx-dynamic.txt
```
## Enumeration via permutation and alterations using alterx
```bash
echo domain.com | alterx -pp 'word=subdomains-top1million-50000.txt' | dnsx > alterx-permutation.txt
```
### Merging all output files into a single file and remove duplicates
```bash
cat *.txt | anew domain.com-subdomains.txt
```
### Filter live subdomains using httpx
```bash
cat domain.com-subdomains.txt | httpx -o httpx.txt
```