## Introduction
The Cyber Kill Chain is a framework created by Lockheed Martin for the cybersecurity industry in 2011. It is based on the "kill chain" military concept. The framework defines the steps used by adversaries or threat actors in the cyberspace. For an adversary to succeed, an adversary needs to go through all phases of the Kill Chain.
![[cyber-kill-chain.png]]
## Importance
The Cyber Kill Chain helps defenders understand and protect against ransomware attacks, security breaches, and attacks from Advanced Persistent Threats (APTs). The Kill Chain can be used to assess the security of your network and systems by identifying missing security controls and closing certain security gaps in your infrastructure.

Essentially, understand the kill chain helps defenders, such as SOC Analysts, Threat Hunters, Incident Responders, and Security Researchers, recognize the intrusion attempts and understand the intruder's goals and objectives.
## Reconnaissance
Reconnaissance is discovering and collecting information on the system and the victim. The reconnaissance phase is the planning phase for the adversaries.

OSINT or open-source intelligence falls under recon phase. It is usually the first step an adversary needs to complete to carry our further phases of an attack. An adversary needs to study their victim by collecting every available piece of information, including size, email addresses, phone numbers, and employees from publicly available sources.
### Email Harvesting
Email harvesting is the process of obtaining email addresses from public, paid, or free services. An attacker can use email-address harvesting for a phishing attack. The adversary will use several arsenal of tools to conduct this phase, including but not limited to:
- [theHarvester](https://github.com/laramies/theHarvester) - other than gathering emails, this tool is also capable of gathering names, subdomains, IPs, and URLs using multiple public data sources 
- [Hunter.io](https://hunter.io/) - this is  an email hunting tool that will let you obtain contact information associated with the domain
- [OSINT Framework](https://osintframework.com/) - OSINT Framework provides the collection of OSINT tools based on various categories
### Social Media Harvesting
Adversaries may also use social media websites such as Facebook, X (Twitter), LinkedIn, and Instagram to collect information on a specific victim. The information found on social media can be beneficial for an attacker to conduct a phishing attack.
## Weaponization
After a successful recon phase, adversaries would then work on crafting a "weaponizer", which combines a malware and an exploit into a deliverable payload. Most adversaries will use automated tools to generate the malware or refer to the DarkWeb to purchase the malware. More sophisticated actors or nation-sponsored APTs would write their own custom malware to make the malware sample unique and bypass some defenses.

In the Weaponization phase, the attacker would:
- Create an infected Microsoft Office document containing a malicious macro or VBA (Visual Basic for Applications) scripts.
- An attacker can create a malicious payload or a very sophisticated worm, implant it on the USB drives, and then distribute them in public. 
- An attacker would choose Command and Control (C2) techniques for executing the commands on the victim's machine or deliver more payloads.
- An attacker would select a **backdoor** implant (the way to access the computer system, which includes bypassing the security mechanisms.
## Delivery
The Delivery phase is when adversaries decides to choose the method for transmitting the payload or the malware. Some options that adversaries commonly use are:
- **Phishing email**: After determining the target for the attack, adversaries would craft malicious email that would target a specific or multiple target. The email would contain a payload or malware.
- **Distributing infected USB drives in public places**: Some adversaries might decide to conduct a sophisticated USB Drop Attack by printing the company's logo on the USB drives and mailing them to the company while pretending to be a customer sending the USB devices as a gift.
- **Watering hole attack**: A watering hole attack is a targeted attack designed to aim at a specific group of people by compromising the website they are usually visiting and then redirecting them to the malicious website of an attacker's choice.
## Exploitation
After gaining access to the system, adversaries could exploit software, system, or server-based vulnerabilities to escalate the privileges or perform lateral movement through the network. Lateral movement are techniques used by adversaries to move deeper into a network to obtain sensitive data.

Adversaries might also apply a zero-day exploit or vulnerability, which is an unknown exploit in the wild that exposes a vulnerability in a software or hardware and can create complicated problems well before anyone realizes something is wrong. Often, this type of attacks leaves no opportunity for detection at the beginning.

These are examples of how an attacker carries out exploitation:
- The victim triggers the exploit by opening the email attachment or clicking on a malicious link.
- Using a zero-day exploit.
- Exploit software, hardware, or even human vulnerabilities. 
- An attacker triggers the exploit for server-based vulnerabilities.
## Installation