## Introduction
Snort is an open-source Network Intrusion Detection and Prevention System (NIDS/NIPS). It was developed and still maintained by Martin Roesch, open-source contributors, and the Cisco Talos team.

Snort uses a series of rules that help define malicious network activity and uses those rules to find packets that match against them and generate alerts for the users.
## Capabilities
- Live traffic analysis
- Attack and probe detection
- Packet logging
- Protocol analysis
- Real-time alerting
- Modules & plugins
- Pre-processors
- Cross-platform support! (Linux & Windows)
## Modes
Snort has three main modes:
- **Sniffer Mode**: Read IP packets like `tcpdump` and prompt them in the console application.
- **Packet Logger Mode**: Log all IP packets (inbound and outbound) that visit the network.
- **NIDS and NIPS Mode**: Log/drop the packets that are deemed malicious according to rules.
## Common Commands
### Configuration Validity
```bash
snort -c /etc/snort/snort.conf -T
```
The `-c` parameter identifies the config file, while the `-T` is Snort's self-test parameter.
### Sniffer Mode: With Parameter "-i" and "-v"
```bash
snort -i eth0 -v
```
Starts the Snort instance in verbose mode (`-v`) and define the network interface to sniff/listen (`-i`).
### Sniffer Mode: With Parameter "-d" and "-e"
```bash
snort -d -e
```
Starts the Snort instance in dumping packet mode (`-d`) and link-layer header grabbing mode (`-e`).
### Sniffer Mode: With Parameter "-X"
```bash
snort -X
```
Starts the Snort instance in full packet dump mode (`-X`). This will also i
### Packet Logger Mode: With Parameter "-l"
```bash
snort -dev -l .
```
Starts the Snort instance in packet logger mode and creates the logs in the current directory. The logs that are created requires specialize tools like `tcpdump` to be read.
### Packet Logger Mode: With Parameter "-K ASCII"
```bash
snort -dev -K ASCII -l .
```
Starts the Snort instance in packet logger mode and creates logs in ASCII format, which makes it human-readable without using a specialized tool.
### Packet Logger Mode: With Parameter "-r"
```bash
snort -r snort.log [icmp/tcp/udp]
```
Starts the Snort instance in packet reader mode (`-r`). Note that, logs created with the `-K ASCII` format parameter can't be read by this command. This command also allows the user to filter the log files.

The parameter `-n` can also be added to determine how many packets will be read. For example `-n 10` will process only the first 10 packets.