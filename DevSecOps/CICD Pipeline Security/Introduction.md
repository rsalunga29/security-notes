Establishing a secure build environment is crucial to safeguarding your software development process against potential threats and vulnerabilities.
## Fundamentals of CI/CD
There are eight fundamentals of CI/CD according to GitLab. These are:
1. **A single source repository** - Source code management should be used to store all the necessary files and scripts required to build the application.
2. **Frequent check-ins to the main branch** - Code updates should be kept smaller and performed more frequently to ensure integrations occur as efficiently as possible.
3. **Automated builds** - Build should be automated and executed as updates are being pushed to the branches of the source code storage solution.
4. **Self-testing builds** - As builds are automated, there should be steps introduced where the outcome of the build is automatically tested for integrity, quality, and security compliance.
5. **Frequent iterations** - By making frequent commits, conflicts occur less frequently. Hence, commits should be kept smaller and made regularly.
6. **Stable testing environments** - Code should be tested in an environment that mimics production as closely as possible.
7. **Maximum visibility** - Each developer should have access to the latest builds and code to understand and see the changes that have been made.
8. **Predictable deployments anytime** - The pipeline should be streamlined to ensure that deployments can be made at any time with almost no risk to production stability.
## Typical CI/CD Pipeline
1. **Developer workstations** - Where the coding magic happens, developers craft and build code.
2. **Source code storage solution** - The central storage to store and track different source code versions. GitLab and GitHub are an example of this.
3. **Build orchestrator** - Coordinates and manages the automation of the build and deployment environments. GitLab and Jenkins are an example of build orchestrator servers.
4. **Build agents** - These machines build, test and package the code. GitLab Runners and Jenkins Agents are an example of build agents.
5. **Environments** - There are development stages, and there are environments for these stages. These are typically, development, testing/staging, and production. The code is built and validated through the stages.