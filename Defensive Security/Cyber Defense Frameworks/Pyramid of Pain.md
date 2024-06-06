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

The knowledge of the IP addresses a threat actor uses can be valuable. The most common defense tactic is to block, drop, or deny inbound requests from these IP addresses on the perimeter or firewall.