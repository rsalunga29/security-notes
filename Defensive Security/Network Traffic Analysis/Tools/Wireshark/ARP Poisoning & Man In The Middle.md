Address Resolution Protocol (ARP) is the technology responsible for allowing devices to identify themselves on a network.

ARP Poisoning also known as ARP Spoofing or Man In The Middle (MITM) attack is a type of attack that involves network jamming/manipulating by sending malicious ARP packets to the default gateway. The ultimate aim is to manipulate the **"IP to MAC address table"** and sniff the traffic of the target host.
## ARP Flags

| **Notes**                                                                                                                                                                                                                                          | **Wireshark filter**                                                                                                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Global search                                                                                                                                                                                                                                      | - `arp`                                                                                                                                                                                                                                                |
| "ARP" options for grabbing the low-hanging fruits:<br><br>- Opcode 1: ARP requests.<br>- Opcode 2: ARP responses.<br>- **Hunt:** Arp scanning<br>- **Hunt:** Possible ARP poisoning detection<br>- **Hunt:** Possible ARP flooding from detection: | - `arp.opcode == 1`<br><br>- `arp.opcode == 2`<br><br>- `arp.dst.hw_mac==00:00:00:00:00:00`<br><br>- `arp.duplicate-address-detected or arp.duplicate-address-frame`<br><br>- `((arp) && (arp.opcode == 1)) && (arp.src.hw_mac == target-mac-address)` |
## ARP Analysis
A suspicious situation means having two different ARP responses (conflict) for a particular IP address.

Knowing the network architecture and inspecting the traffic for a specific time frame can help detect the anomaly.
![[arp-analysis-1.png]]
Look at the given picture; there is a conflict; the MAC address that ends with "b4" crafted an ARP request with the "192.168.1.25" IP address, then claimed to have the "192.168.1.1" IP address. Here we have our notes below:

| **Notes**                      | Detection Notes                                                                                                              | **Findings**                                            |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Possible IP address match.     | 1 IP address announced from a MAC address.                                                                                   | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.25          |
| Possible ARP spoofing attempt. | 2 MAC addresses claimed the same IP address (192.168.1.1).  <br>The " 192.168.1.1" IP address is a possible gateway address. | - MAC1: 50:78:b3:f3:cd:f4<br>- MAC 2: 00:0c:29:e2:18:b4 |
| Possible ARP flooding attempt. | The MAC address that ends with "b4" claims to have a different/new IP address.                                               | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.1           |
> Note: Taking notes of our findings before going any further will help us be organized and make it easier to correlate further findings.