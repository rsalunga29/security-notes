## Event Correlation
Event correlation refers to the identification of significant relationships of different artefacts from different log sources such as application logs, endpoint logs, and network logs, and connecting each related artefacts.

For example, a network connection log may exist in various log sources such as Sysmon logs (Event ID 3: Network Connection) and Firewall Logs. The Firewall log may provide the source and destination IP, source and destination port, protocol, and the action taken. In contrast, Sysmon logs may give the process that invoked the network connection and the user running the process.

With this information, we can connect the dots of each artefact from the two data sources:

- Source and Destination IP
- Source and Destination Port
- Action Taken
- Protocol
- Process name
- User Account
- Machine Name

Event correlation can build the puzzle pieces to complete the exact scenario from an investigation.
## Baselining
Baselining is the process of knowing what is expected to be normal. It usually requires a vast amount of data-gathering to establish the standard behavior of user activities, network traffic across infrastructure, and processes running on all machines owned by the organization.