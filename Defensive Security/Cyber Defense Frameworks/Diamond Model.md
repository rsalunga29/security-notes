## Introduction
The Diamond Model of Intrusion Analysis is a framework developed by Sergio Caltagirone, Andrew Pendergast, and Christopher Betz in 2013. It's composed of four core features: Adversary, Infrastructure, Capability, and Victim.

The Diamond Model carries the essential concepts of identifying and analyzing intrusion and adversary operations while allowing the flexibility to expand and integrate new ideas and concepts. It also provides various opportunities to integrate intelligence in real-time for network defense, automating correlation across events, classifying events with confidence into adversary campaigns, and forecasting adversary operations while planning and gaming mitigation strategies.
## Socio-Political
The socio-political component of the Diamond Model describes the needs and intent of the adversary. For example, financial gain, hacktivism, or espionage.
## Adversary
The term adversary in this model, is an actor or organization responsible for utilizing a capability against the victim to achieve their intent. It is also known as an attacker, enemy, cyber threat actor, or hacker. The adversary is the person who stands behind the cyberattack.

Adversary knowledge can generally be mysterious, and this core feature is likely to be empty for most events – at least at the time of discovery.

It is often difficult to identify an adversary during the initial stages of a cyber attack. However, by utilizing data collected from an incident or breach, artifacts or signatures, and other relevant information, we may be able to determine who the adversary might be.
### Adversary Operator
An adversary operator is the "hacker" or person(s) conducting the intrusion activity.
### Adversary Customer
An adversary customer is an entity that stands to benefit from the activity conducted in the intrusion. It may be the same person who stands behind the adversary operator, or it may be a separate person or group.
## Victim
A victim is the target of the adversary. It can be a person, organization, target email addresses, IP addresses, domains, etc.

A victim can be an opportunity for the attackers to get a foothold on the organization they are trying to attack. There is always a victim in every cyberattack.
### Victim Personae
A victim personae are the people and organizations being targeted and whose assets are being attacked and exploited.
### Victim Assets
A victim assets are the attack surface and includes the victim's systems, networks, email addresses, IP addresses, user account, etc., to which the adversary will direct their capabilities.
## Capability
Capability is the skill, tools, and techniques used by the adversary in the intrusion activity. The capability also highlights the adversary's tactics, techniques, and procedures (TTPs).

The capabilities can be malware and phishing email development skills or, at least, access to capabilities, such as acquiring malware or ransomware as a service.
### Capability Capacity
Refers to all of the vulnerability and weaknesses that the individual capability can use.
### Adversary Arsenal
Refers to the set of capabilities that belong to an adversary. The combined capacities of an adversary's capabilities make it the adversary's arsenal.
## Infrastructure
The infrastructure is the physical or logical interconnections that the adversary uses to deliver a capability or maintain control of capabilities. It can be a software or a hardware. For example, a command and control server or the results from the victim (data exfiltration).

The infrastructure can also be IP addresses, domain names, email addresses, or even a malicious USB device found in the street that is being plugged into a workstation.\
### Type 1 Infrastructure
Refers to the infrastructure controlled or owned by the adversary.
### Type 2 Infrastructure
Refers to the infrastructure controlled by an intermediary that is used by the adversary. In some cases, this is the infrastructure that the victim will see as the adversary, and the intermediary might or might not be aware of it.

Type 2 Infrastructures are used by adversaries to obfuscate the source and attribution of the intrusion. It includes malware staging servers, malicious domain names, compromised email accounts, etc.
### Service Providers
Refers to the organization that provides services considered critical for the adversary. For example, internet service providers, domain registrars, and webmail providers.
## Event Meta Features
Six possible meta-features can be added to the Diamond Model. Meta-features are not required, but they can add some valuable information or intelligence to the Diamond Model.
### Timestamp
Refers to the time and date of the intrusion event. Each event can be recorded with a date and time that it occurred, such as 2021-09-12 02:10:12.136. It can also include when the event started and stopped. Timestamps are essential to help determine the patterns and group the malicious activity.
### Phase
"Every malicious activity contains two or more phases which must be successfully executed in succession to achieve the desired result."

The phases of an intrusion, attack, or breach. A great example can be the [Cyber Kill Chain](obsidian://open?vault=security-notes&file=Defensive%20Security%2FCyber%20Defense%20Frameworks%2FCyber%20Kill%20Chain) or [Unified Kill Chain](obsidian://open?vault=security-notes&file=Defensive%20Security%2FCyber%20Defense%20Frameworks%2FUnified%20Kill%20Chain).
### Result
The event results can be labelled as "success," "failure," or "unknown." The event results can also be related to the CIA (confidentiality, integrity, and availability) triad, such as Confidentiality Compromised, Integrity Compromised, and Availability Compromised.

Another approach can also be documenting all of the post-conditions resulting from the event.

It is crucial to capture the results and post-conditions of an adversary's operations, but sometimes they might not always be known.
### Direction
Helps describe host-based and network-based events and represents the direction of the intrusion attack. The Diamond Model of Intrusion Analysis defines seven potential values:
1. Victim-to-Infrastructure
2. Infrastructure-to-Victim
3. Infrastructure-to-Infrastructure
4. Adversary-to-Infrastructure
5. Infrastructure-to-Adversary
6. Bidirectional
7. Unknown
### Methodology
This meta-feature will allow an analyst to describe the general classification of intrusion, for example, phishing, DDoS, breach, port scan, etc. 
### Resources
"Every intrusion event requires one or more external resources to be satisfied prior to success."

Examples of the resources can include the following:
1. Software (e.g operating systems, virtualization software, or Metasploit framework)
2. Knowledge (e.g how to use Metasploit, how to perform Lateral Movement)
3. Information (e.g username/password to masquerade)
4. Hardware (e.g servers, workstations, routers)
5. Funds (e.g money to purchase domains or servers)
6. Facilities (e.g electricity or shelter)
7. Access (e.g network path from host to victim and vice versa)