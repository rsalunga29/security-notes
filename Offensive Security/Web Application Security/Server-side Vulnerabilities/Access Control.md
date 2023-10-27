Access control is the application of constraints on who or what is authorized to perform actions or access resources. In the context of web applications, access control is dependent on authentication and session management:
- **Authentication** confirms that the user is who they say they are
- **Session management** identifies which subsequent HTTP requests are being made by the same user
- **Access control** determined whether the user is allowed to carry out the action they are attempting to perform

 Broken access controls are common and often present a critical security vulnerability. Design and management of access controls is a complex and dynamic problem that applies business, organizational, and legal constraints to a technical implementation. Access control design decisions have to be made by humans so the potential for errors is high.
## Vertical vs Horizontal Privilege Escalation
Vertical privilege escalation is, when a user can gain access to functionality that they are not permitted to access. An example of vertical privilege escalation is, when a non-administrative user can access an admin page where they can modify or delete user accounts.

Horizontal privilege escalation is,
## Unprotected Functionality
Vertical privilege escalation usually happens when an application does not enforce protection for sensitive functionality. For example, admin functions linked to an admin page but not from a regular user page. However, a user might be able to access the admin functions and page by browsing the relevant admin URL.
```txt
https://target-website.com/administration
```
In some cases, admin URLs might be disclosed in other locations such as `robots.txt`:
```txt
https://target-website.com/robots.txt
```
And even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality.