## Advantages
### Availability of Network-based Evidences
Network-based evidences are usually easier to capture and collect compared to logs, IOCs, etc..
### Noise-Free Data/Evidence Collection
Network traffic is less noisy and more manageable compared to investigating unfiltered events from EDRs, EPPs, and log systems.
### Durability
Network traffic is challenging to destroy as it is the transferred data. Although it can be hidden through encryption, tunneling and packet manipulation.
### Availability of Log Sources
Logs provide valuable information which helps to correlate the chain of events and support the investigation hypothesis.
### Detecting Memory and Non-Residential Malicious Activities
Network forensics tools can identify threats residing in memory and non-residential malware through analysis of command sequences and network connections.
## Disadvantages
### Decision-making Challenges
One of the most difficult challenges of network forensics is determining the course of action. Network forensics can serve various purposes like SOC, IR, and Threat Hunting.
### Sufficient Data/Evidence Collection
While network forensics ease the collection of evidences, it can be overwhelming. Multiple factors must be considered when gathering data/evidence from the network.
### Limited Data Capture
Capturing all network activity is not applicable and operable. So, it is hard always to have the packet captures that covers pre, during and post-event. 
### Incomplete Full-Packet Capture
Continuously capturing, storing, and processing full packets costs a lot of time and resources. This inability to perform continuous full-packet capture creates time gaps in data, resulting in missing a significant part of an event.
### Encrypted Traffic
Discovering the contents of encrypted data is impossible. However, it can still provide valuable information such as source and destination IP and port, and used services.
### Privacy Concerns in Traffic Recording
Capturing the traffic is the same as "recording everything on the wire"; therefore, this act should comply with GDPR and business-specific regulations (e.g. HIPAA, PCI DSS and FISMA).
### Non-standard Port Usage
Threat actors sometimes use non-standard ports and services to avoid detection abd
### Timezone issues
### Lack of Logs
