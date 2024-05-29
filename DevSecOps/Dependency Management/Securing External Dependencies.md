## Public CVEs
The team that develops external dependencies can also make mistakes. This means there may be vulnerabilities in the code that they have written. The issue, however, is that these vulnerabilities will be publicly disclosed, usually as a Common Vulnerabilities and Exposures (CVE), once the developers have created a patch.

While this is good practice to ensure that dependency developers are fixing security issues, for team that uses the dependency, it's a problem. As the specific version of their dependency is now vulnerable to an issue that is visible online, even to attackers.

As such, it is important for developers to patch the relevant dependency as soon as possible. But this is easier said than done, as dependencies are usually version locked for stability. So upgrading to a new version means, developers need to first determine is the upgrade could cause instability. The problem gets even worse when you start to talk about dependencies of dependencies. It is perhaps not the SDK that you are using that is vulnerable, but a dependency of the SDK, that is. Since that dependency has to be updated, we will also now need to update our SDK.
## Supply Chain Attacks
Even if applications are well-secured and hardened, attackers can still compromise them by targeting dependencies, which might be developed by smaller team with limited security budgets. These indirect attacks are called supply chain attacks.

Supply chains attacks are even more effective since a dependency might be used by several applications. Meaning the compromise of a single dependency could lead to the compromise of several applications.

One APT group, namely MageCart, was notorious for performing these types of attacks. Some highlights of their actions:
- Compromising the payment portal of British Airways' online portal led to the compromise of credit cards of customers and a fine for BA of 230 million dollars.
- Compromising more than 100000 customers' credit cards by embedding skimmers in various payment portals of various applications.
- Compromising more than 10000 AWS S3 buckets and embedding malware in any JavaScript found in these buckets.
## Defenses
It's often difficult to defend against attacks on external dependencies since there are so many and new vulnerabilities are found daily. However, there are certain things we can do to limit the risk:
- Make sure to update and patch dependencies on a regular basis, including emergency patching in the event a serious vulnerability is discovered.
- Dependencies can sometimes be copied and hosted internally. This will reduce the attack surface.
- Sub-resource Integrity can be used to prevent tampered JS libraries from loading. In the HTML include, the hash of the JS library can be added. Modern web browsers will verify the hash of the JS library, and if it does not match, the library will not be loaded.
