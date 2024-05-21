## Dependency Management
The first step to securing the build process is to [secure the dependencies](obsidian://open?vault=security-notes&file=DevSecOps%2FDependency%20Management) of the build. Most source code nowadays depend on external libraries and SDKs for their functionalities. During a build process, the pipeline will gather the dependencies to perform the build.
## When to Start the Build?
The CI/CD pipelines and the build process is remote code execution as a feature. Once a pipeline starts, the build server communicates with one of the build agents to perform the build, which includes reading the commands that have to be executed from the CI/CD instruction file and performing them.

While this creates automation, it also creates the risks that if an attacker is able to access the CI/CD instruction files and alter what is being built or the commands that are being executed, they may leverage it to compromise systems.

Answering the following three questions can help understand the attack surface of a pipeline:
### What actions to start the build process?
We have the ability to determine what actions can start the build process. This can be non-strict as allowing the pipeline to start every time a code is committed, or more stricter
### Who can start the build process?
After deciding which actions can start the build process, it is important to narrow down who can perform such actions. 
### Where will the build process occur?
Lorem
## How to Secure the Build Process
Lorem Ipsum la