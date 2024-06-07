## Introduction
The Unified Kill Chain, published in 2017, provides deeper insights into each stage of an attack by linking specific techniques from the ATT&CK framework to each phase of the traditional kill chain (Cyber Kill Chain).

The UKC states that there are 18 phases to an attack: Everything from reconnaissance to data exfiltration and understanding an attacker's motive. These phases have been grouped together in this note into a few areas of focus for brevity, which will be detailed in the remaining tasks.
![[unified-kill-chain.png]]
## Phase In: Initial Foothold
The main focus of this series of phases is for an attacker to gain access to a system or networked environment. An attacker will employ numerous tactics to investigate the system for potential vulnerabilities that can be exploited to gain a foothold in the system.

The different actions of this phase are the following:
### Reconnaissance ([MITRE Tactic TA0043](https://attack.mitre.org/tactics/TA0043/))
Techniques that an adversary employs to gather information relating to their target. This can be achieved through means of passive and active reconnaissance.

Information gathered from this phase can include:
- Discovering what systems and services are running on the target.
- Finding contact lists or lists of employees that can be impersonated or used in either a social engineering or phishing attack.
- Looking for potential credentials that may be of use in later stages, such as pivoting or initial access.
- Understanding the network topology and other networked systems can be used to pivot too.
### Weaponization ([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))
In this phase, the adversary will set up the necessary infrastructure to perform the attack. For example, a command & control server or a system capable of catching reverse shells and delivering payloads to the target systems.
### Social Engineering ([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))
Techniques that an adversary can employ to manipulate employees to perform actions that will aid in their attack. For example, a social engineering attack could include:
- Getting a user to open a malicious attachment.
- Impersonating a web page and having the user enter their credentials.
- Calling or visiting the target and impersonating a user or being able to gain access to areas of a site that the attacker would not previously be capable of.
### Exploitation ([MITRE Tactic TA0002](https://attack.mitre.org/tactics/TA0002/))
T
## Phase Through: Network Propagation
Lorem
## Phase Out: Action on Objectives
Lorem