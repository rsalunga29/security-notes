DNS Zone Transfer is a form of DNS enumeration in which an attacker attempts to replicate a zone file from the primary DNS server into a secondary DNS server.

A zone file is a database containing a list of all the domain names and corresponding IP addresses registered on the server.

For an attacker, this is a useful enumeration trick as it can reveal information about an internal network infrastructure of an organization. It can also allows them to launch various attacks such as phishing scams, spamming, and domain hijacking.

This vulnerability is caused by a misconfigured DNS server, which causes anyone to request the zone file. To remediate, the DNS server must be configured properly to only allow the replicating DNS server to have access to the zone file.
## Host, Dig, and Nslookup
1. Enumerate the nameservers of the target domain by using any of the following commands:
	- `host -t ns target.com`
	- `dig ns target.com`
	- `nslookup -type=ns target.com`
1. Test for `AXFR` zone transfer using any of the following commands:
	- `host -l target.com ns.target.com`
	- `dig axfr target.com @ns.target.com`
	- `nslookup -type=any -query=axfr target.com ns.target.com`
## DNSrecon
```nix
dnsrecon -d target.com -t axfr
```
