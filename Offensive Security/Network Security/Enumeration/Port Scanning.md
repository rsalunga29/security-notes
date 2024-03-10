## Most Common Ports
### Nmap TCP
```bash
nmap -sC -sV -oN nmap/initial -vv 10.10.10.10 # add -sS if you want it to be stealthy
```
### Nmap UDP
```bash
nmap -sU -sV -oN nmap/initial -vv 10.10.10.10
```
### Autorecon
```bash
autorecon 10.10.10.10 -vv
```
```bash
autorecon --target-file target-ips.txt
```
## All Open Ports
### Nmap
```bash
nmap -sC -sV -oN nmap/allports -p- -T4 --min-rate=9326 -vv 10.10.10.10  # add -sS if you want it to be stealthy
```
### Masscan
```bash
masscan -p1–65535 10.10.10.10
```
### Rustscan
```bash
rustscan -a 10.10.10.10 --ulimit 5000 -- -A # This will only show open ports, services & versions wont be shown
```
## Advanced Port Scanning
### Stealthy TCP NULL Scan
```bash
nmap -sN -vv 10.10.10.10
```
### Stealthy TCP SYN Scan
```bash
nmap -sS -vv 10.10.10.10
```
### IP Spoofing
Spoofed IP: `10.10.10.11`
```bash
nmap -e eth0 -Pn -S 10.10.10.11 10.10.10.10
```
### MAC Spoofing
```bash
nmap -Pn --spoof-mac A0:10:A0:10 10.10.10.10
```
### Decoy Technique
Decoys `10.10.11.11` and `10.10.12.12`
`RND` refers to random IPs, `ME` refers to our IP
```bash
nmap -Pn -D 10.10.11.11,10.10.12.12,RND,ME 10.10.10.10
```
### Zombie Scan
Example: `10.10.5.5` is a printer
```bash
nmap -sI 10.10.5.5 10.10.10.10 # Idle IP: 10.10.5.5 in this example is a rarely used printer
```