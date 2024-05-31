The dependency confusion was discovered by Alex Birsan in 2021. This type of attack is a race condition created by an attacker that could lead to a malicious dependency being used instead of internal one.

The issue stems from how internal dependencies are managed. When we run `pip install numpy`, `pip` will connect to the external PyPi repository to look for a package called `numpy`, find the latest version, and install it. If we wanted to install an internal package, we can actually use the `--extra-index-url` argument to specify an additional PyPi server, for example:
```bash
pip install numpy --extra-index-url http://internal.pypi-server.com/
```
But what if `numpy` exists in both the internal repo and the external, public-facing PyPi repo? How does pip know which package to install? Well, it's simple, it will collect the package from all available repos, compare the version numbers, and then install the package with the highest version number.
## Staging An Attack