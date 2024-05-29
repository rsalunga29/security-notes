## Public CVEs
The team that develops external dependencies can also make mistakes. This means there may be vulnerabilities in the code that they have written. The issue, however, is that these vulnerabilities will be publicly disclosed, usually as a Common Vulnerabilities and Exposures (CVE), once the developers have created a patch.

While this is good practice to ensure that dependency developers are fixing security issues, for team that uses the dependency, it's a problem. As the specific version of their dependency is now vulnerable to an issue that is visible online, even to attackers.

As such, it is important for developers to patch the relevant dependency as soon as possible. But this is easier said than done, as dependencies are usually version locked for stability. So upgrading to a new version means, developers need to first determine is the upgrade could cause instability. The problem gets even worse when you start to talk about dependencies of dependencies. It is perhaps not the SDK that you are using that is vulnerable, but a dependency of the SDK, that is. Since that dependency has to be updated, we will also now need to update our SDK.
## Supply Chain Attacks
Even if applications are well-secured and hardened, attackers can still compromise them by targeting dependencies, which might be developed by smaller team with limited security budgets. These indirect attacks are called supply chain attacks.

One APT group, namely MageCart, was notorious for performing these types of attacks. Some highlights of their actions:
