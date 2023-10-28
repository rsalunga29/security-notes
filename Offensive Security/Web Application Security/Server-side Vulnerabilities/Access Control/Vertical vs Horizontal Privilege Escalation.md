Vertical privilege escalation is, when a user can gain access to functionality that they are not permitted to access. An example of a vertical privilege escalation is, when a non-administrative user can access an admin page where they can modify or delete user accounts.

Horizontal privilege escalation is, when a user is able to gain access to resources belonging to another user, instead of their own resources. An example of a horizontal privilege escalation is, when an user can access the records of other users as well as their own.

Horizontal and vertical privilege escalation attacks may use similar types of exploit methods. For example, a user might access their own account page and another user's account page by modifying the `id` parameter in the following URL:
```txt
https://target-website.com/account?id=123
```
The above is an example of an [Insecure Direct Object Reference (IDOR)](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FAccess%20Control%2FInsecure%20Direct%20Object%20Reference) vulnerability.