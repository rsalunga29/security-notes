explain here

identify name server `nslookup -type=ns target.com`
test for ANY and AXFR zone transfer `nslookup -type=any -query=AXFR target.com nameserver.target.com` or `dig axfr target.com @nameserver.target.com`