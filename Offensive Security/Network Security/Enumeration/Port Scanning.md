# Most Common Ports

## Nmap TCP

```nix
nmap -sC -sV -oN nmap/initial -vv 10.10.10.10 # add -sS if you want it to be stealthy
```

## Nmap UDP

```nix
nmap -sU -sV -oN nmap/initial -vv 10.10.10.10
```

## Autorecon

```nix
autorecon 10.10.10.10 -vv
```

```nix
autorecon --target-file target-ips.txt
```

# All Open Ports

## Nmap

```nix
nmap -sC -sV -oN nmap/allports -p- -T4 --min-rate=9326 -vv 10.10.10.10  # add -sS if you want it to be stealthy
```

## Masscan

```nix
masscan -p1–65535 10.10.10.10
```

## Rustscan

```nix
rustscan -a 10.10.10.10 --ulimit 5000 -- -A # This will only show open ports, services & versions wont be shown
```

# Advanced Port Scanning

## Stealthy TCP NULL Scan

```nix
nmap -sN -vv 10.10.10.10
```

## Stealthy TCP SYN Scan

```nix
nmap -sS -vv 10.10.10.10
```

## IP Spoofing

Spoofed IP: `10.10.10.11`

```nix
nmap -e eth0 -Pn -S 10.10.10.11 10.10.10.10
```

## MAC Spoofing

```nix
nmap -Pn --spoof-mac A0:10:A0:10 10.10.10.10
```

## Decoy Technique

Decoys `10.10.11.11` and `10.10.12.12`

`RND` refers to random IPs, `ME` refers to our IP

```nix
nmap -Pn -D 10.10.11.11,10.10.12.12,RND,ME 10.10.10.10
```

## Zombie Scan

Example: `10.10.5.5` is a printer

```nix
nmap -sI 10.10.5.5 10.10.10.10 # Idle IP: 10.10.5.5 in this example is a rarely used printer
```