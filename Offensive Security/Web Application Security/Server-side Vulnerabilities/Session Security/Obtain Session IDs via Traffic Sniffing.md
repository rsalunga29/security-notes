Traffic sniffing is something that most penetration testers do when assessing a network's security from the inside. They usually do this by plugging their laptops or other tools into available ethernet ports. Doing so allows them to monitor the traffic and gives them an idea of the traffic going through the network and the services they may attack. This means that traffic sniffing can only be performed if the attacker and the victim are on the same local network.

Obtaining session identifiers through traffic sniffing requires:
- The attacker must be positioned on the same local network as the victim.
- Unencrypted HTTP traffic.

There are numerous packet sniffing tools, the most popular one is [Wireshark](https://www.wireshark.org/), which already have a built-in filter function that allows users to filter traffic for specific protocols such as HTTP, SSH, FTP, and even for a particular source IP address.