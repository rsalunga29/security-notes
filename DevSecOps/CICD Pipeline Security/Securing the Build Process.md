## Dependency Management
The first step to securing the build process is to secure the dependencies of the build. Most source code nowadays depend on external libraries and SDKs for their functionalities. During a build process, the pipeline will gather the dependencies to perform the build. There are two main concerns when it comes to dependencies.

1. **Supply Chain Attacks**: If a threat actor can take over one of these dependencies, they would be able to inject malicious code into the build.
2. **Dependency Confusion**: If an internally developed dependency is used, an attacker could attempt a dependency confusion attack to inject code into the build process itself.