## Dependency Management
The first step to securing the build process is to [secure the dependencies](obsidian://open?vault=security-notes&file=DevSecOps%2FDependency%20Management) of the build. Most source code nowadays depend on external libraries and SDKs for their functionalities. During a build process, the pipeline will gather the dependencies to perform the build.
## When to Start the Build?
The CI/CD pipelines and the build process is remote code execution as a feature. Once a pipeline starts, the build server communicates with one of the build agents to perform the build, which includes reading the commands that have to be executed from the CI/CD instruction file and performing them.

While this creates automation, it also creates the risks that if an attacker is able to access the CI/CD instruction files and alter what is being built or the commands that are being executed, they may leverage it to compromise systems.
### What actions start the build p
## How to Secure the Build Process
Lorem Ipsum la