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
## Save into Log File
Alternatively, we can also opt to save the PCAP as log files first before continuing with our investigation:
```bash
snort -c [rule_file] -r investigate.pcap -X -l .
```
We can also use this technique if we are getting the error "Warning: No preprocessor configured for policy 0."
## Filtering Results
Filtering results is easy, we just need to add the filter query at the end of the command. For example:
```bash
snort -c /etc/snort/snort.conf -r snort.log.timestamp -A cmg 'tcp and port 80'
```
```bash
snort -c local.rules -r snort.log.timestamp -A fast 'udp'
```
### Using `strings` to Filter Results
Use the Linux `strings` command to look for specific string in the Snort log:
```bash
strings snort.log.timestamp | grep "string-im-looking-for"
```
## Number of Rules Triggered
Look for the "Limits" keyword on the Snort output. This is just below the "Action Stats" results.
## Look for SID of Triggered Rules
```bash
cat snort.log.timestamp | grep -r -e sid
```