The primary structure of the snort rule is shown below:
![[snort-rule-structure.png]]
## Action Types
There are several actions for rules. The most common are listed below:
- **alert**: Generate an alert and log the packet.
- **log**: Log the packet.
- **drop**: Block and log the packet.
- **reject**: Block the packet, log it and terminate the packet session.
## Protocol Types
Snort2 only supports the following protocols:
- IP
- TCP
- UDP
- ICMP
However, if we want to detect traffic from specific applications, say FTP, we cannot use the "FTP" keyword in the Protocol field, instead we will filter the FTP traffic by investigating TCP traffic on port 21.
## Direction
