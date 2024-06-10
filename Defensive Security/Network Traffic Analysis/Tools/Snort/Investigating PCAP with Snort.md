Capabilities of Snort are not limited to sniffing, logging and detecting/preventing the threats. PCAP read/investigate mode helps you work with PCAP files.
## Read Single PCAP
```bash
snort -c /etc/snort/snort.conf --pcap-single=investigate.pcap -A [console/cmg/full/fast/none]
```
## Read Multiple PCAPs
```bash
snort -c /etc/snort/snort.conf --pcap-list="investigate.pcap mal.pcap phish.pcap" -A [console/cmg/full/fast/none]
```
Adding the `--pcap-show` parameter at the end would distinguish each PCAP for easier viewing.