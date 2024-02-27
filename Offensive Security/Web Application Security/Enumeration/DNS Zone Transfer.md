DNS Zone Transfer is a form of DNS enumeration in which an attacker attempts to replicate or copy a DNS database or a zone file from the primary DNS server into a secondary DNS server.

A zone file is a database containing a list of all the domain names and corresponding IP addresses registered on the server.

For an attacker, this is a useful enumeration trick as it can reveal information about an internal network infrastruc

identify name server `nslookup -type=ns target.com`
test for ANY and AXFR zone transfer `nslookup -type=any -query=AXFR target.com nameserver.target.com` or `dig axfr target.com @nameserver.target.com`