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
> Note: Once Snort is started running in IDS/IPS mode, the sniffing and logging mode will be semi-passive. However, functions can still be activate using various parameters (i.e `-i`, `-v`, `-d`, `-e`, `-X`, `-l`, `-K ASCII`, etc.)