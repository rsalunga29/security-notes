Capabilities of Snort are not limited to sniffing, logging and detecting/preventing the threats. PCAP read/investigate mode helps you work with PCAP files.
## Read Single PCAP
```bash
snort -c /etc/snort/snort.conf --pcap-single=investigate.pcap -A [console/cmg/full/fast/none] '[filter]'
```
> Note: Alternative to `--pcap-single` is `-r`.
## Read Multiple PCAPs
```bash
snort -c /etc/snort/snort.conf --pcap-list="investigate.pcap mal.pcap phish.pcap" -A [console/cmg/full/fast/none] '[filter]'
```
Adding the `--pcap-show` parameter at the end would distinguish each PCAP for easier viewing.
## Filtering Results
Filtering results is easy, we just need to add the filter query at the end of the command. For example:
```bash
snort -c /etc/snort/snort.conf -r investigate.pcap -A full 'tcp and port 80'
```
```bash
snort -c /etc/snort/snort.conf -r malware.pcap -A fast 'udp'
```