## Nmap
### ICMP Ping
```bash
nmap -sn -PE 10.10.10.0/24
```
### ARP Ping
```bash
nmap -sn -PR 10.10.10.0/24
```
### TCP/SYN Ping
```bash
nmap -sn -PS 10.10.10.0/24
```
### UDP Ping
```bash
nmap -sn -PU 10.10.10.0/24
```
## FPing
```bash
fping -g -r 1 10.10.10.0/24
```
## ARP-Scan
```bash
arp-scan --localnet
```
```bash
arp-scan 10.10.10.0/24
```
## Receive Ping
Useful for testing if target server can reach our attack box
```bash
tcpdump -i INTERFACE icmp
```