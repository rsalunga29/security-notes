This menu provides multiple statistics options ready to investigate to help users see the big picture in terms of the scope of the traffic, available protocols, endpoints and conversations, and some protocol-specific details like DHCP, DNS and HTTP/2.
## Resolved Addresses
This option helps analysts identify IP addresses and DNS names available in the capture file by providing the list of the resolved addresses and their hostnames. The hostname information is taken from DNS answers in the capture file.

You can use the **"Statistics --> Resolved Addresses"** menu to view all resolved addresses by Wireshark.
## Protocol Hierarchy
This option breaks down all available protocols from the capture file and helps analysts view the protocols in a tree view based on packet counters and percentages.

You can use the **"Statistics --> Protocol Hierarchy"** menu to view this info.\
## Conversations
Conversation represents traffic between two specific endpoints. This option provides the list of the conversations in five base formats; ethernet, IPv4, IPv6, TCP and UDP.

You can use the "Statistic --> Conversations" menu to view this info.
## Endpoints
The endpoints option is similar to the conversations option. The only difference is that this option provides unique information for a single information field (Ethernet, IPv4, IPv6, TCP and UDP ).

Wireshark also supports resolving MAC addresses to human-readable format using the manufacturer name assigned by IEEE. This only works for the known manufacturers as conversion is done through the first 3 bytes of the MAC address.

You can use the "Statistics --> Endpoints" menu to view this info.
## IP Geolocation Mapping
Besides name resolution, Wireshark also provides an IP geolocation mapping that helps analysts identify the map's source and destination addresses. Currently, Wireshark supports MaxMind databases, and the latest versions of the Wireshark come configured MaxMind DB resolver.

This option can be enabled by using the "Edit --> Preferences --> Name Resolution --> MaxMind database directories" menu.
## IPv4 and IPv6
The statistics menu has two options for narrowing the statistics on packets containing a specific IP version.

You can use the "Statistics --> IPvX Statistics" menu to view this info.
## DNS
This option breaks down all DNS packets from the capture file and helps analysts view the findings in a tree view based on packet counters and percentages of the DNS protocol.

You can use the "Statistics --> DNS" menu to view this info.
## HTTP
This option breaks down all HTTP packets from the capture file and helps analysts view the findings in a tree view based on packet counters and percentages of the HTTP protocol.

You can use the "Statistics --> HTTP" menu to view this info.