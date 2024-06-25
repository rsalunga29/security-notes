Wireshark is an open-source, cross-platform network packet analyser tool capable of sniffing and investigating live traffic and inspecting PCAPs. It is one of the best packet analysis tool.
## Nmap Scans
### TCP Flags

| **Notes**                                                                                | **Wireshark Filters**                                                      |
| ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Global search.                                                                           | - `tcp`<br>- `udp`                                                         |
| - Only SYN flag.<br>- SYN flag is set. The rest of the bits are not important.           | - `tcp.flags == 2`<br>- `tcp.flags.syn == 1`                               |
| - Only ACK flag.<br>- ACK flag is set. The rest of the bits are not important.           | - `tcp.flags == 16`<br>- `tcp.flags.ack == 1`                              |
| - Only SYN, ACK flags.<br>- SYN and ACK are set. The rest of the bits are not important. | - `tcp.flags == 18`<br>- `(tcp.flags.syn == 1) and (tcp.flags.ack == 1)`   |
| - Only RST flag.<br>- RST flag is set. The rest of the bits are not important.           | - `tcp.flags == 4`<br>- `tcp.flags.reset == 1`                             |
| - Only RST, ACK flags.<br>- RST and ACK are set. The rest of the bits are not important. | - `tcp.flags == 20`<br>- `(tcp.flags.reset == 1) and (tcp.flags.ack == 1)` |
| - Only FIN flag<br>- FIN flag is set. The rest of the bits are not important.            | - `tcp.flags == 1`<br>- `tcp.flags.fin == 1`                               |
| -                                                                                        | - `tcp.flags.syn == 1 and tcp.flags.ack == 0 and tcp.window_size > 1024`   |
### TCP Connect Scans
- Relies on the three-way handshake (needs to finish the handshake process).
- Usually conducted with `nmap -sT` command.
- Used by non-privileged users (only option for a non-root user).
- Usually has a windows size larger than 1024 bytes as the request expects some data due to the nature of the protocol.

| **Open TCP Port**                        | **Open TCP Port  <br>**                                    | **Closed TCP Port**         |
| ---------------------------------------- | ---------------------------------------------------------- | --------------------------- |
| - SYN --><br>- <-- SYN, ACK<br>- ACK --> | - SYN --><br>- <-- SYN, ACK<br>- ACK --><br>- RST, ACK --> | - SYN --><br>- <-- RST, ACK |
### TCP SYN Scans
- Doesn't rely on the three-way handshake (no need to finish the handshake process).
- Usually conducted with `nmap -sS` command.
- Used by privileged users.
- Usually have a size less than or equal to 1024 bytes as the request is not finished and it doesn't expect to receive data.

| **Open TCP Port**                      | **Close TCP Port**         |
| -------------------------------------- | -------------------------- |
| - SYN --><br>- <-- SYN,ACK<br>- RST--> | - SYN --><br>- <-- RST,ACK |
### UDP Scans
- Doesn't require a handshake process.
- No prompt for open ports.
- ICMP error message for close ports.
- Usually conducted with `nmap -sU` command.

| Open UDP Port    | Closed UDP Port                                                                                |
| ---------------- | ---------------------------------------------------------------------------------------------- |
| - UDP packet --> | - UDP packet --><br>- ICMP Type 3, Code 3 message. (Destination unreachable, port unreachable) |
