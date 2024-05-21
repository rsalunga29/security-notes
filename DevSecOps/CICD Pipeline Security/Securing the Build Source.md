The first step to securing a pipeline is to secure the source code. In the event a threat actor (TA) can compromise the source code, they are in position to compromise the pipeline itself. We want to protect our source code from two main issues:
### Unauthorized Tampering
Only authorized users should be able to make changes to the source code. This means that we want to control who has the ability to push new code to our repo.
### Unauthorized Disclosure
Depending on the application, the source code might be considered sensitive information. In situations where this is the case, we must ensure that the source code is not intentionally or accidentally disclosed to the public.
### Confusion of Responsibilities
Another common mistake made by large organizations is believe that the perimeter is a sufficient security boundary. This false belief can lead to several security issues, such as weak authentication and authorization mechanisms, sensitive information exposure, privilege escalation, and many more.

Below are some example scenarios:

**Leaving the registration open for their self-hosted GitLab server**
Even if GitLab is hosted inside an intranet, if registration is open to any users within the intranet, the attack surface would grow significantly. If a single employee has been compromised, an attacker would have the ability to register an account and exfiltrate any publicly shared repos.

**Repositories are shared publicly**
Some may even believe that since the GitLab server is hosted inside the intranet, it's okay to configured repos to be shared publicly. However, this would mean that any user who has a valid GitLab account will be able to view and modify any source code within the repositories.

Furthermore, an attacker with a GitLab account will be able to use GitLab API to automate the process of discovering and exfiltrating publicly available repositories.
### How to Secure the Build Source
Following the principle of least privilege by implementing granular access control is the key. This ensures that different users or groups have only the enough permissions and restrictions to perform their task. This helps maint