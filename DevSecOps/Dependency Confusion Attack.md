The dependency confusion was discovered by Alex Birsan in 2021. This type of attack is a race condition created by an attacker that could lead to a malicious dependency being used instead of internal one.

The issue stems from how internal dependencies are managed. When we run `pip install numpy`, `pip` will connect to the external PyPi repository to look for a package called `numpy`, find the latest version, and install it. If we wanted to install an internal package, we can actually use the `--extra-index-url` argument to specify an additional PyPi server, for example:
```bash
pip install numpy --extra-index-url http://internal.pypi-server.com/
```
But what if `numpy` exists in both the internal repo and the external, public-facing PyPi repo? How does pip know which package to install? Well, it's simple, it will collect the package from all available repos, compare the version numbers, and then install the package with the highest version number.
## Staging An Attack
All an attacker really needs to stage an internal dependency attack is the name of one of your internal dependencies. Names of internal dependencies can be accidentally leaked by:
- Developers who ask questions in public forum but do not obfuscate sensitive information such as the names of libraries being used.
- Some compiled applications like NodeJS will often disclose internal package names in their `package.json`.

Once an attacker learns the name of an internal dependency, they can attempt to host a package with a similar name on one of the external package repos but with a higher version number. This will force any application that attempts to install this dependency to get confused between the internal and external package. If the external one is chosen, the attack will succeed.
![[dependency-confusion-attack.png]]