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
The phase describes how an adversary abuse system weaknesses or vulnerabilities to perform code execution. Including, but not limited to:
- Uploading and executing a reverse shell to a web application.
- Interfering with an automated script on the system to execute code.
- Abusing a web application vulnerability to execute code on the system it is running on.
### Persistence ([MITRE Tactic TA0003](https://attack.mitre.org/tactics/TA0003/))
In this phase, the adversary will perform several techniques to maintain their access to the compromised system. For example:
- Creating a service on the target system that will allow the attacker to regain access.
- Adding the target system to a Command & Control server where commands can be executed remotely at any time.
- Leaving other forms of backdoors that execute when a certain action occurs on the system (i.e. a reverse shell will execute when a system administrator logs in).
### Defense Evasion ([MITRE Tactic TA0005](https://attack.mitre.org/tactics/TA0005/))
This phase specifically is used to understand the techniques an adversary uses to evade defensive measures put in place in the system or network. For example:
- Web application firewalls
- Network firewalls
- Anti-virus systems
- Intrusion detection and prevention systems
### Command & Control ([MITRE Tactic TA0011](https://attack.mitre.org/tactics/TA0011/))
An adversary can establish command and control of a target system to achieve its action on objectives. For example, the adversary can:
- Execute commands.
- Steal data, credentials and other information.
- Use the controlled server to pivot to other systems on the network.
### Pivoting ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))
"Pivoting" is the technique an adversary uses to reach other systems within a network that are not otherwise accessible from the internet. These systems often contain valuable data or have weaker security.
## Phase Through: Network Propagation
This phase follows a successful foothold being established on the target network. An attacker would seek to gain additional access and privileges to systems and data to fulfil their goals.

The different actions of this phase are the following:
### Pivoting ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))
Once the attacker has access to the system, they would use it as as the distribution point for all malware and backdoors at later stages.
### Discovery ([MITRE Tactic TA0007](https://attack.mitre.org/tactics/TA0007/))
The adversary would uncover information about the system and the network it is connected to, such as active user accounts, account permissions, applications and software installed, files, directories, and system configurations.
### Privilege Escalation ([MITRE Tactic TA0004](https://attack.mitre.org/tactics/TA0004/))
Following their information gathering, adversaries would attempt to gain increased privileges/permissions within the pivot system. They would often leverage misconfigurations and vulnerabilities found to elevate their access to one of the following superior levels:
- SYSTEM/ ROOT.
- Local Administrator.
- A user account with Admin-like access.
- A user account with specific access or functions.
### Execution ([MITRE Tactic TA0002](https://attack.mitre.org/tactics/TA0002/))
In this phase, the adversary would deploy their malicious code using the pivot system as their host. Remote trojans, C2 scripts, malicious links and scheduled tasks are deployed and created to facilitate a recurring presence on the system and uphold their persistence.
### Credential Access ([MITRE Tactic TA0006](https://attack.mitre.org/tactics/TA0006/))
Working hand in hand with the Privilege Escalation stage, the adversary would attempt to steal account names and passwords through various methods, including keylogging and credential dumping. This would make it harder for defenders to detect any attack as legitimate credentials are being used.
### Lateral Movement ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))
With the credentials and elevated privileges, the adversary would seek to move through the network and jump onto other targeted systems to achieve their primary objective. The stealthier the technique used, the better.
## Phase Out: Action on Objectives
The final phase an adversary's attack on an environment, where they have critical asset access and can fulfil their attack goals. These goals are usually geared toward compromising the confidentiality, integrity and availability (CIA) triad.

The different actions of this phase are the following:
### Collection ()