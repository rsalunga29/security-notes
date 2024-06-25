Address Resolution Protocol (ARP) is the technology responsible for allowing devices to identify themselves on a network.

ARP Poisoning also known as ARP Spoofing or Man In The Middle (MITM) attack is a type of attack that involves network jamming/manipulating by sending malicious ARP packets to the default gateway. The ultimate aim is to manipulate the **"IP to MAC address table"** and sniff the traffic of the target host.
## ARP Flags

| **Notes**                                                                                                                                                                                                                                          | **Wireshark filter**                                                                                                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Global search                                                                                                                                                                                                                                      | - `arp`                                                                                                                                                                                                                                                |
| "ARP" options for grabbing the low-hanging fruits:<br><br>- Opcode 1: ARP requests.<br>- Opcode 2: ARP responses.<br>- **Hunt:** Arp scanning<br>- **Hunt:** Possible ARP poisoning detection<br>- **Hunt:** Possible ARP flooding from detection: | - `arp.opcode == 1`<br><br>- `arp.opcode == 2`<br><br>- `arp.dst.hw_mac==00:00:00:00:00:00`<br><br>- `arp.duplicate-address-detected or arp.duplicate-address-frame`<br><br>- `((arp) && (arp.opcode == 1)) && (arp.src.hw_mac == target-mac-address)` |
## Example ARP Analysis
A suspicious situation means having two different ARP responses (conflict) for a particular IP address.

Knowing the network architecture and inspecting the traffic for a specific time frame can help detect the anomaly.
![[arp-analysis-1.png]]
Look at the given picture; there is a conflict; the MAC address that ends with "b4" crafted an ARP request with the "192.168.1.25" IP address, then claimed to have the "192.168.1.1" IP address.

> Note: Taking notes of our findings before going any further will help us be organized and make it easier to correlate further findings.

Here we have our notes below:

| **Notes**                      | Detection Notes                                                                                                             | **Findings**                                            |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Possible IP address match.     | 1 IP address announced from a MAC address.                                                                                  | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.25          |
| Possible ARP spoofing attempt. | 2 MAC addresses claimed the same IP address (192.168.1.1).  <br>The "192.168.1.1" IP address is a possible gateway address. | - MAC1: 50:78:b3:f3:cd:f4<br>- MAC 2: 00:0c:29:e2:18:b4 |
| Possible ARP flooding attempt. | The MAC address that ends with "b4" claims to have a different/new IP address.                                              | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.1           |
A flood of ARP requests could be a sign of a malicious activity, scan or network problems. Look at the given picture below, it is evident that there is a new anomaly.
![[arp-analysis-2.png]]
The MAC address that ends with "b4" crafted multiple ARP requests with the "192.168.1.25" IP address. We update our notes with:

| Notes                          | Detection Notes                                                                                    | Findings                                        |
| ------------------------------ | -------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| Possible ARP flooding attempt. | The MAC address that ends with "b4" crafted multiple ARP requests against a range of IP addresses. | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.xxx |
Based on our notes and findings, we can so far conclude that the MAC address that ends with "b4" owns the "192.168.1.25" IP address and crafted suspicious ARP requests against a range of IP addresses. It also claimed to have the possible gateway address as well.
### Correlating with Other Protocols
Checking the HTTP traffic, everything look normal at the IP level, but if we added the MAC addresses as columns, we can see there is another anomaly.
![[arp-analysis-3.png]]
The MAC address that ends with "b4" is the destination of all HTTP packets! A clear evidence of a MITM attack, and the attacker is the MAC address that ends with "b4".
### Conclusion
Our final notes and findings are as follows:

| Detection Notes    | Findings                                        |                                                                                                                                         |
| ------------------ | ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| IP to MAC matches. | 3  IP to MAC address matches.                   | - MAC: 00:0c:29:e2:18:b4 = IP: 192.168.1.25<br>- MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.1<br>- MAC: 00:0c:29:98:c7:a8 = IP: 192.168.1.12 |
| Attacker           | The attacker created noise with ARP packets.    | - MAC: 00:0c:29:e2:18:b4 = IP: 192.168.1.25                                                                                             |
| Router/gateway     | Gateway address.                                | - MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.1                                                                                               |
| Victim             | The attacker sniffed all traffic of the victim. | - MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.12                                                                                              |
