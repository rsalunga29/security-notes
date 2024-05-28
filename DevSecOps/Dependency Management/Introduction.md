## What is a Dependency?
Modern applications make extensive use of libraries and Software Development Kits (SDKs) that assist with the basic (and sometimes complex) features of the application, allowing the developer to focus purely on the key features and functionality of the application.

These libraries and SDKs are called dependencies. While dependencies make our lives a lot easier, they have to be securely managed since they now form part of the overall attack surface of the application.
## What is Dependency Management?
Dependency management is the process of managing your dependencies through your SDLC process and DevOps pipeline. We perform dependency management for several reasons:
- Knowing what dependencies our application uses can allow us to support it better.
- We often want to version lock dependencies to improve the stability of our application since newer versions may add new features or deprecate features that our application actively uses.
- We can build golden images that already have all our dependencies installed, meaning we can perform faster deployment cycles.
- When new developers are onboarded, we can help them set up their development machine by installing all the required dependencies.
- We can monitor the dependencies we use for security issues to ensure that dependencies are upgraded with the security fixes as needed.
## Dependency Management Tools
Most large organizations use tools for dependency management, such as [JFrog Artifactory](https://jfrog.com/artifactory/). These type of tools allows an organization to manage all of their dependencies in a central location and makes it easier for dependency management to be integrated into a CI/CD pipeline.