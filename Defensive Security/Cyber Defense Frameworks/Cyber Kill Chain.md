## Introduction
The Cyber Kill Chain is a framework created by Lockheed Martin for the cybersecurity industry in 2011. It is based on the "kill chain" military concept. The framework defines the steps used by adversaries or threat actors in the cyberspace. For an adversary to succeed, an adversary needs to go through all phases of the Kill Chain.
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
After a successful recon phase, adversaries would then work on crafting a 