## Nmap
### ICMP Ping
```nix
nmap -sn -PE 10.10.10.0/24
```
### ARP Ping
```nix
nmap -sn -PR 10.10.10.0/24
```
### TCP/SYN Ping
```nix
nmap -sn -PS 10.10.10.0/24
```
### UDP Ping
```nix
nmap -sn -PU 10.10.10.0/24
```
## FPing
```nix
fping -g -r 1 10.10.10.0/24
```
## ARP-Scan
```nix
arp-scan --localnet
```
```nix
arp-scan 10.10.10.0/24
```
## Receive Ping
Useful for testing if target server can reach our attack box
```nix
tcpdump ip proto \\\\icmp
```