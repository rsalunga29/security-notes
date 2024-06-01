## Hardening
### Pod Hardening
Some best practices for pod security include:
- Containers that run applications should not have root privileges.
- Containers should have an immutable filesystem, meaning they cannot be altered or added to (depending on the purpose of the container, this may not be possible).
- Container images should be frequently scanned for vulnerabilities or misconfigurations.
- Privileged containers should be prevented.
- [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/) and [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/).
### Network Isolation
By default, pods can communicate with one another. To ensure this communication is secure, the following best practices can be followed:
- Access to the control plane node should be restricted using a firewall and role-based access control in an isolated network.
- Control plane components should communicate using Transport Layer Security (TLS) certificates.
- An explicit deny policy should be created.
- Credentials and sensitive information should not be stored as plain text in configuration files. Instead, they should be encrypted and in Kubernetes secrets.
### Properly Implemented Authentication and Authorization
Here are some best practices which can help make sure you are making efficient use of Kubernetes authentication and authorisation features:
- Anonymous access should be disabled.
- Strong user authentication should be used.
- RBAC policies should be created for the various teams using the cluster and the service accounts utilized.
### Monitoring and Logging
Here are some logging best practices to ensure you know exactly what is going on in your cluster and can detect threats when they appear:
- Audit logging should be enabled.
- A log monitoring and alerting system should be implemented.
### Patch Management
- Security patches and updates should be applied quickly.
- Vulnerability scans and penetration tests should be done regularly to assess security controls effectiveness.
- Any obsolete components in the cluster should be removed.
## Security Best Practices
### Implementing RBAC
Role-based Access Control (RBAC) in Kubernetes regulates access to a Kubernetes cluster and its resources based on defined roles and permissions. These are assigned to users, groups or service accounts. RBAC can be configured using a YAML file (same as defining a resource) where specific rules can be defined by declaring the resource type and verbs. Verbs are the actions being restricted, such as 'create' and 'get'.
### Secrets Management
A Kubernetes secret is an object used to store sensitive information (like credentials, OAuth tokens or SSH keys). Secrets are stored as a base64 encoded string, unencrypted by default. For security, it is best to configure encryption at rest. Another way to promote secure secrets management in your Kubernetes cluster is to configure the least privilege access to secrets using RBAC.
### Pod Security Standards (PSS) and Pod Security Admission (PSA)
Pod Security Standards are used to define security policies at 3 levels (privileged, baseline and restricted) at a namespace or cluster-wide level. What these levels mean:
- **Privileged**: This is a near unrestricted policy (allows for known privilege escalations).
- **Baseline**: This is a minimally restricted policy and will prevent known privilege escalations (allows deployment of pods with default configuration).
- **Restricted**: This heavily restricted policy follows the current pod hardening best practices.

Pod Security Admission (using a Pod Security Admission controller) enforces the Pod Security Standards by intercepting API server requests and applying these policies.

>Note: Previously, the roles of PSA and PSS were fulfilled using PSPs (Pod Security Policies); however, as of Kubernetes v1.25, these have been removed.