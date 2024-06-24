Brim is an open-source desktop application that processes PCAP files and log files, with a primary focus in providing search and analytics. Brim is founded by Steve McCanne who is also the created of PCAP and bpf.

BRIM is built on open-source platforms:
- **Zeek**: Log generating engine.
- **Zed Language**: Log querying language that allows performing keyword searches with filters and pipelines.
- **ZNG Data Format**: Data storage format that supports saving data streams.
- **Electron and React**: Cross-platform UI.

Brim uses the Zeek log processing format and supports Zeek signatures and Suricata Rules for detection.

It can handle two types of data as input:
- Packet Capture Files: Pcap files created with tcpdump, tshark and Wireshark like applications.
- Log Files: Structured log files like Zeek logs.
## Why Brim?
Brim reduces the time and effort spent processing and investigating PCAP files larger than 1GB, in which Wireshark is slow.
## Brim vs Wireshark vs Zeek
While each of them is powerful and useful, each tool has its own strength and weaknesses. The common best practice is handling medium-sized pcaps with Wireshark, creating logs and correlating events with Zeek, and processing multiple logs in Brim.
# Tutorial
Visit [TryHackMe - Brim](https://tryhackme.com/r/room/brim).