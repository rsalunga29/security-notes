## Subdomains
### GoBuster
```nix
gobuster dns -d target.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
### Ffuf
```nix
ffuf -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://FUZZ.target.com -ic
```
### Sublist3r
```nix
python3 sublist3r.py -d target.com -b -p 80,443,21 -v
```
### Subfinder
```nix
subfinder -d target.com
```
### Nslookup
```nix
nslookup -type=any target.com
```
### Crt.sh using Curl
```nix
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
```nix
export TARGET="target.com"

cat sources.txt | while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}_${TARGET}";done
```
Extract and sort all found subdomains
```nix
cat *.json | jq -r '.hosts[]' 2>/dev/null | cut -d':' -f 1 | sort -u > "${TARGET}_theHarvester.txt"
```
## VHosts
### GoBuster
```nix
gobuster vhosts –u target.com –w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
### Ffuf
```nix
ffuf -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://target.com -H "Host: FUZZ.target.com" -ic
```