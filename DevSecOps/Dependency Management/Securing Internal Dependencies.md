## Similarity of Concerns with External Dependencies
Internal dependencies have similar concerns as external dependencies, if a dependency has a vulnerability, it will affect internal applications that is using that dependency. Therefore, we have to perform security testing of our dependencies before they are released for use.
## Legacy Code
Another issue is that internal dependencies can become legacy code incredibly fast. For example, if the developer that created and maintained a dependency has left the company, the dependency will no longer receive updates. If such a dependency is used in several applications, it can become an issue if a vulnerability is discovered.

This problem can only be made worse if the documentation is not kept up to date. Making it hard for someone new to take responsibility for the dependency.
## Storage and Access Control
A unique security concern to internal dependencies is storage. We want to ensure that a dependency can be accessed by all developers for use, but not modification. If all developers can simply modify the dependency, an attacker would simply have to compromise a single developer to compromise several applications.