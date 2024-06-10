Some are the most common supply chain attack techniques used in the past:
- **Typosquatting** - An attacker hosts a package called `nunpy`, hoping that a developer will mistype the name and install their malicious package.
- **Source Injection** - An attacker contributes to the package for a new feature through a pull request but also embeds a vulnerability in the code that could be used to compromise applications that make use of the package.
- **Domain Expiry** - Sometimes, the developers of packages may forget to renew the domain where their email is being hosted. If this happens, an attacker can buy the expired domain, allowing them full control over email, which could be used to reset the password of a package maintainer to gain full control over the package. This is a common risk for legacy packages on these external repositories.