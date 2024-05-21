The first step to securing a pipeline is to secure the source code. In the event a threat actor (TA) can compromise the source code, they are in position to compromise the pipeline itself. We want to protect our source code from two main issues:
## Unauthorized Tampering
Only authorized users should be able to make changes to the source code. This means that we want to control who has the ability to push new code to our repo.
## Unauthorized Disclosure
Depending on the application, the source code might be considered sensitive information. In situations where this is the case, we must ensure that the source code is not intentionally or accidentally disclosed to the public.
## Confusion of Responsibilities
Another common mistake made by large organizations is believe that the perimeter is a sufficient security boundary. This false belief can lead to several security issues, such as weak authentication and authorization mechanisms, sensitive information exposure, privilege escalation, and many more.

Below are some example scenarios:

**Leaving the registration open for their self-hosted GitLab server**
Even if GitLab is hosted inside an intranet, if registration is open to any users within the intranet, the attack surface would grow significantly. If a single employee has been compromised, an attacker would have the ability to register an account and exfiltrate any publicly shared repos.

**Repositories are shared publicly**
Some may even believe that since the GitLab server is hosted inside the intranet, it's okay to configured repos to be shared publicly. However, this would mean that any user who has a valid GitLab account will be able to view and modify any source code within the repositories.

Furthermore, an attacker with a GitLab account will be able to use GitLab API to automate the process of discovering and exfiltrating publicly available repositories.
## How to Secure the Build Source
Following the principle of least privilege by implementing granular access control is the key. This ensures that different users or groups have only the enough permissions and restrictions to perform their task. This helps ensure the security, confidentiality, and integrity of the source code while maintaining effective collaboration within a development environment.

In our example, GitLab has several features that simplifies permission management across multiple repositories and projects:
1. **Group-based Access Control**: GitLab allows users to organize projects into groups, which allows permission management at a group-level instead of project-level. This approach reduces the chances of errors and oversights when configuring permissions for individual repositories.
2. **Access Levels**: GitLab offers different access levels, such as Guest, Reporter, Developer, Maintainer, and Owner. Each level comes with specific capabilities and permissions.
3. **GitLab's .gitignore**: This file specifies which files or directories should be excluded from version control.  This prevents sensitive data like passwords, API keys, and configuration files from being committed into the repositories.
4. **Environment Variables**: GitLab allows users to define and management environment variables securely, separate from the source code. This is useful for storing sensitive data needed during the CI/CD process.
5. **Branch Protection**: Branches, like master or main, can be protected to prevent direct pushes, ensuring that changes go through code review and automated testing before merging.

Additionally, it is also important to follow best practices to protect the security of your source code:
- Review and update access permissions regularly as team members change roles or leave the organisation.
- Implement two-factor authentication (2FA) to add an extra layer of security to user accounts.
- Monitor audit logs to track who has accessed or modified repositories and projects.
- Regularly scan repositories for sensitive information using tools designed for this purpose.