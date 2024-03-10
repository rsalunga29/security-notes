## Subdomains
### GoBuster
```bash
gobuster dns -d target.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
### Ffuf
```bash
ffuf -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://FUZZ.target.com -ic
```
### Sublist3r
```bash
python3 sublist3r.py -d target.com -b -p 80,443,21 -v
```
### Subfinder
```bash
subfinder -d target.com
```
### Nslookup
```bash
nslookup -type=any target.com
```
### Crt.sh using Curl
```bash
export TARGET="target.com"

curl -s "https://crt.sh/?q=${TARGET}&output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u > "${TARGET}_crt.sh.txt"
```
### theHarvester
Create a `sources.txt` list using the following content:
- baidu
- bufferoverun
- crtsh
- hackertarget
- otx
- projectdiscovery
- rapiddns
- sublist3r
- threatcrowd
- trello
- urlscan
- vhost
- virustotal
- zoomeye
Run the command
```bash
export TARGET="target.com"

cat sources.txt | while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}_${TARGET}";done
```
Extract and sort all found subdomains
```bash
cat *.json | jq -r '.hosts[]' 2>/dev/null | cut -d':' -f 1 | sort -u > "${TARGET}_theHarvester.txt"
```
## VHosts
### GoBuster
```bash
gobuster vhosts –u target.com –w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
### Ffuf
```bash
ffuf -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://target.com -H "Host: FUZZ.target.com" -ic
```