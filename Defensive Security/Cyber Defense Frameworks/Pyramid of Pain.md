## Introduction
The Pyramid of Pain is a conceptual model which may be used to detect indicators of compromised and actions of attackers. It can be used to improve the effectiveness of Cyber Threat Intelligence, Incident Response, and Threat Hunting.
![[pyramid-of-pain.png]]
## Hash Values (Trivial)
A hash value is a numeric value of a fixed length that uniquely identifies data. It is the result of a hashing algorithm. Security professionals usually use the hash values to gain insights into a specific malware sample, a malicious or a suspicious file, and as a way to unique identify and reference the malicious artifact.

The following are the most common hashing algorithms:
1. **MD5 (Message Digest)**: Designed by Ron Rivest in 1992 and is a widely used cryptographic hash function with a 128-bit hash value. MD5 hashes are not considered cryptographically secure.
2. **SHA-1 (Secure Hash Algorithm 1)**: Invented by the NSA in 1995. When data is fed to the SHA-1 algorithm, the algorithm takes the input and produces a 160-bit hash value string as a 40 digit hexadecimal number. NIST deprecated the use of SHA-1 in 2011 and banned its use for digital signatures at the end of 2013 based on it being susceptible to brute-force attacks.
3. **SHA-2 (Secure Hash Algorithm 2)**: The SHA-2 algorithm was invented by NIST and NSA in 2001 designed to replace SHA-1. SHA-2 has many variants, and arguably the most common is SHA-256 which returns a hash value of 256-bits as a 64 digit hexadecimal number.

A hash is not considered to be cryptographically secure if two files have the same hash value or digest.

Various online tools can be used to do hash lookups like [VirusTotal](https://www.virustotal.com/gui/) and [Metadefender Cloud - OPSWAT](https://metadefender.opswat.com/?lang=en).
## IP Address (Easy)
An IP address is used to identify any device connected to a network. These devices range from desktops, servers, and even CCTV cameras. We rely on IP addresses to send and receive the information over the network.

The knowledge of the IP addresses an adversary uses can be valuable. The most common defense tactic is to block, drop, or deny inbound requests from these IP addresses on the perimeter or firewall. This tactic is often not bulletproof as it’s trivial for an experienced adversary to recover simply by using a new public IP address.
### Fast Flux
Fast Flux is a DNS technique of having multiple IP addresses associated with a domain name, which is constantly changing. This technique is primarily used by adversaries or botnets to hide phishing, web proxying, malware delivery, and malware C2 activities. As a result of this, defenders find it challenging to carry out successful IP blocking.
## Domain Names (Simple)
Domain Names can be thought as simply mapping an IP address to a string of text. A domain name can contain a domain and a top-level domain ([evilcorp.com](http://evilcorp.com/)) or a sub-domain followed by a domain and top-level domain ([tryhackme.evilcorp.com](http://tryhackme.evilcorp.com/)).

Domain names can be a little more of a pain for the attack to change, as they would most likely need to purchase a domain and modify its DNS records. However, many DNS providers have loose standards and provide APIs to make it easier for the attacker to change the domains.

To detect the malicious domains, proxy logs or web server logs can be used.
### Punycode
Punycode attack is used by attackers to redirect users to a malicious domain that seems legitimate at first glance. Punycode is a way of converting words that cannot be written in ASCII, into a Unicode ASCII encoding. For example, the URL `adıdas.de` has the Punycode of `http://xn--addas-o4a.de/`.

Modern browsers such as Google Chrome, Microsoft Edge, and Apple Safari are now pretty good at translating the obfuscated characters into the full punycode domain name.
### URL Shorteners
One technique used by adversaries to hide malicious domains are URL Shorteners.  URL Shortener is a tool that creates a short and unique URL that will redirect to the specific website specified during the initial step of setting up the URL Shortener link. Adversaries usually use the following URL shortening services:
- bit.ly
- goo.gl
- ow.ly
- s.id
- smarturl.it
- tiny.pl
- tinyurl.com
- x.co

One technique to see the actual URL of the shortened link is by appending `+`. For example:
- **tiny.url**: http://tinyurl.com/zzzxxxyyy+
- **bit.ly**: http://bit.ly/111222333+
- **goo.gl**: http://goo.gl/aaabbbccc+
## Host / Network Artifacts (Annoying)
Host artifacts are the traces or observables that attackers leave on the system, such as registry values, suspicious process execution, attack patterns or IOCs (Indicators of Compromise), files dropped by malicious applications, or anything exclusive to the current threat.

A network artifact can be a user-agent string, C2 information, or URI patterns followed by the HTTP POST requests.An attacker might use a User-Agent string that hasn’t been observed in your environment before or seems out of the ordinary. These artifacts can be detected in Wireshark PCAPs by using a network protocol analyzer such as [TShark](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) or exploring IDS (Intrusion Detection System) logging from a source such as [Snort](https://www.snort.org/).

Adversaries will feel a little more annoyed or frustrated if their attack is detected at this level. As they will likely need to change their tactics and methodology, or modify the tools. This gives defenders ample time to respond and detect the upcoming threats or remediate existing ones.
## Tools (Challenging)
Adversaries would use the utilities to create malicious macro documents (maldocs) for spearphishing attempts, a backdoor that can be used to establish [C2 (Command and Control Infrastructure)](https://www.varonis.com/blog/what-is-c2/), any custom .EXE, and .DLL files, payloads, or password crackers.

AV signatures, detection rules, and YARA rules can be a great weapons against attackers at this stage. [MalwareBazaar](https://bazaar.abuse.ch/) and [Malshare](https://malshare.com/) are good resources that provides access with samples, malicious feeds, and YARA results, which can be helpful when it comes to threat hunting and incident response.

For detection rules, [SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/) is a great platform, where security professionals share their detection rules for different kinds of threats including the latest CVE's that are being exploited in the wild by adversaries.
### Fuzzy Hashing
Fuzzy hashing (a.k.a context triggered piecewise hashes) is a strong weapon against an adversary's tools. Fuzzy hashing helps perform similarity analysis, which means match two files with minor differences based on the fuzzy hash values. One example of fuzzy hashing is the usage of [SSDeep](https://ssdeep-project.github.io/ssdeep/index.html). 
## TTPs (Tough)
TTPs stands for Tactics, Techniques & Procedures. This includes the whole [MITRE](https://attack.mitre.org/) [ATT&CK Matrix](https://attack.mitre.org/), which means all the steps taken by an adversary to achieve his goal, starting from phishing attempts to persistence and data exfiltration.

If you can detect and respond to the TTPs quickly, you leave the adversaries almost no chance to fight back. For, example if you could detect a [Pass-the-Hash](https://www.beyondtrust.com/resources/glossary/pass-the-hash-pth-attack) attack using Windows Event Log Monitoring and remediate it, you would be able to find the compromised host very quickly and stop the lateral movement inside your network. At this point, the attacker would have two options:
1. Go back, do more research and training, reconfigure their custom tools
2. Give up and find another target