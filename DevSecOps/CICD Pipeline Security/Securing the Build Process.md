## Dependency Management
The first step to securing the build process is to [secure the dependencies](obsidian://open?vault=security-notes&file=DevSecOps%2FDependency%20Management) of the build. Most source code nowadays depend on external libraries and SDKs for their functionalities. During a build process, the pipeline will gather the dependencies to perform the build.
## When to Start the Build?
The CI/CD pipelines and the build process is remote code execution as a feature. Once a pipeline starts, the build server communicates with one of the build agents to perform the build, which includes reading the commands that have to be executed from the CI/CD instruction file and performing them.

While this creates automation, it also creates the risks that if an attacker is able to access the CI/CD instruction files and alter what is being built or the commands that are being executed, they may leverage it to compromise systems.

Answering the following three questions can help understand the attack surface of a pipeline:
### What actions to start the build process?
We have the ability to determine what actions can start the build process. This can be less strict, such as, allowing the pipeline to start every time a code is committed, or more more strict, in which the pipeline only starts if a merge request is made or when code is merged to the master branch.

It is important to understand that allowing multiple actions to start the build process will also increase the attack surface.
### Who can start the build process?
After deciding which actions can start the build process, it is important to narrow down who can perform such actions. In the previous example, the pipeline only starts when the code is merged into the master branch, and users who can approve these merges can be few, reducing the attack surface.

However, if we still want to allow builds to start on creation of a merge request, we have to ensure that the attacker cannot make a merge request or that the merge build will occur in a segregated environment.
### Where will the build process occur?
Finally, it is also important to decide where the build will occur. For example, if we want developers to run builds on other branches, we can just simply register a new build agent specific for that branch, instead of using the build agent for the master branch.

This way, even if the developer branch's build agent is compromised, the build agent for the master branch is untouched.
## How to Secure the Build Process
An insecure build can enable living-off-the-land attacks, supply chain attacks and a lot of trouble that is difficult to detect later in the pipeline. Below are some of the best practices to follow:
1. **Isolation and Containerization**: Run builds in isolated containers to prevent interference and maintain consistency.
2. **Least Privilege**: Grant minimal permissions to CI/CD tools, restricting unnecessary access to sensitive resources.
3. **Secret Management**: Use CI/CD tools' secret management features to store and inject sensitive data securely.
4. **Immutable Artifacts**: Store build artifacts in a secure registry to prevent tampering and enable easy auditing.
5. **Dependency Scanning**: Integrate dependency scanning to identify and address vulnerabilities in third-party libraries.  
6. **Pipeline as Code**: Define CI/CD pipelines as code, version-controlled alongside the source code.  
7. **Regular Updates**: Keep CI/CD tools and dependencies up to date to address known vulnerabilities.
8. **Logging and Monitoring**: Monitor build logs for unusual activities and integrate them with security monitoring systems.