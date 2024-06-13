Capabilities of Snort are not limited to sniffing, logging and detecting/preventing the threats. PCAP read/investigate mode helps you work with PCAP files.
> Note: `rule_file` can either be `/etc/snort/snort.conf`, `local.rules`, or empty (defaults to `snort.conf`).
## Read Single PCAP
```bash
snort -c [rule_file] --pcap-single=investigate.pcap -A [console/cmg/full/fast/none] '[filter]'
```
> Note: Alternative to `--pcap-single` is `-r`.
## Read Multiple PCAPs
```bash
snort -c [rule_file] --pcap-list="investigate.pcap mal.pcap phish.pcap" -A [console/cmg/full/fast/none] '[filter]'
```
Adding the `--pcap-show` parameter at the end would distinguish each PCAP for easier viewing.
## Filtering Results
Filtering results is easy, we just need to add the filter query at the end of the command. For example:
```bash
snort -c /etc/snort/snort.conf -r investigate.pcap -A full 'tcp and port 80'
```
```bash
snort -c local.rules -r malware.pcap -A fast 'udp'
```
### Using `strings` to Filter More Results
First read the PCAP file in Packet Logger mode and save the logs in the current directory:
```bash
snort -c local.rules -r dos.pcap -l .
```
Then use the Linux `strings` command to look for specific