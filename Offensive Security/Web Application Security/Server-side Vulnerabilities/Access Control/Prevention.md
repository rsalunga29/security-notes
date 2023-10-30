Access control vulnerabilities can be prevented by taking a defense-in-depth approach and applying the following principles:
- Never rely on obfuscation alone for access control
- Unless a resource is intended to be publicly accessible, deny access by default
- Wherever possible, use a single application-wide mechanism for enforcing access controls
- At the code level, make it mandatory for developers to declare the access that is allowed for each resource, and deny access by default
- Thoroughly audit and test access controls to ensure they work as designed