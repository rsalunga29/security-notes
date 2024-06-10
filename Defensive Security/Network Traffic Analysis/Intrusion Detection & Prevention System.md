## Intrusion Detection System (IDS)
IDS is a passive monitoring solution, responsible for generating alerts for each malicious activities/patterns, abnormal incidents, and policy violations. IDS requires user intervention to stop these suspicious events.

There are two main types of IDS systems:
- **Network Intrusion Detection System (NIDS)**: NIDS monitors the traffic flow from various areas of the network. The goal is to investigate traffic on the entire subnet.
- **Host-based Intrusion Detection System (HIDS)**: HIDS monitors the traffic flow from a single endpoint device. The goal is to investigate traffic on a particular device.
## Intrusion Prevention System (IPS)
IPS is an active protective solution responsible for stopping/preventing/terminating malicious activities/patterns, abnormal incidents, and policy violations as soon as the detection is performed. IPS requires less user intervention to stop these suspicious events.

There are four main types of IPS systems:
- **Network Intrusion Prevention System (NIPS)**: NIPS monitors the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet.
- **Host-based Intrusion Prevention System (HIPS)**: HIPS actively protects the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device.
- **Wireless Intrusion Prevention System (WIPS)**: WIPS monitors the traffic flow from of wireless network. The aim is to protect the wireless traffic and stop possible attacks launched from there.
- **Network Behavior Analysis (NBA)**: Works similar with NIPS. Only difference is, behavior-based system requires a training period (baselining) to learn the normal traffic and differentiate the malicious traffic and threats.
## Detection/Prevention Techniques
 There are three main detection and prevention techniques used in IDS and IPS solutions:
 - **Signature-based**: This model helps detect known threats by using/following rules that contain the specific patterns of known malicious traffic.
 - **Behavior-based**: This model helps detect unknown or new threats by comparing patterns with known/normal and unknown/abnormal behaviors.
 - **Policy-based**: This model helps detect policy violations by comparing detected activities with system configuration and security policies.