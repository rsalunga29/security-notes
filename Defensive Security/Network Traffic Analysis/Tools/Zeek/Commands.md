There are two operation options for Zeek. The first one is running it as a service, and the second option is running the Zeek against a pcap. The former allows Zeek to listen to live network traffic, while the latter allows Zeek to be used as a packet investigator.
## ZeekControl
To start Zeek as a service, the "ZeekControl" module needs to be used. ZeekControl requires superuser permissions to be able to be used.
### Status
Retrieves the status of the Zeek service.
```bash
zeekctl status
```
### Start
Starts the Zeek service.
```bash
zeekctl start
```
### Stop
Stops the Zeek service.
```bash
zeekctl stop
```
## Packet Investigator
To process PCAP files with Zeek, we need to run the following command:
```bash
zeek -C -r sample.pcap
```
The following command ignores checksum errors (`-C`) and reads/process the PCAP file (`-r`). This will automatically create logs in the working directory.
### Using Signature Files
Zeek uses [signatures](obsidian://open?vault=security-notes&file=Defensive%20Security%2FNetwork%20Traffic%20Analysis%2FTools%2FZeek%2FSignatures) to have rules and event correlations to find noteworthy activities on the network. To use signatures, we need to append the `-s` parameter. For example:
```bash
zeek -C -r sample.pcap -s sample.sig
```