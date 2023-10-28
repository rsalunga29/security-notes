Access control is the application of constraints on who or what is authorized to perform actions or access resources. In the context of web applications, access control is dependent on authentication and session management:
- **Authentication** confirms that the user is who they say they are
- **Session management** identifies which subsequent HTTP requests are being made by the same user
- **Access control** determined whether the user is allowed to carry out the action they are attempting to perform

 Broken access controls are common and often present a critical security vulnerability. Design and management of access controls is a complex and dynamic problem that applies business, organizational, and legal constraints to a technical implementation. Access control design decisions have to be made by humans so the potential for errors is high.
## Vertical vs Horizontal Privilege Escalation
Vertical privilege escalation is, when a user can gain access to functionality that they are not permitted to access. An example of a vertical privilege escalation is, when a non-administrative user can access an admin page where they can modify or delete user accounts.

Horizontal privilege escalation is, when a user is able to gain access to resources belonging to another user, instead of their own resources. An example of a horizontal privilege escalation is, when an user can access the records of other users as well as their own.

Horizontal and vertical privilege escalation attacks may use similar types of exploit methods. For example, a user might access their own account page and another user's account page by modifying the `id` parameter in the following URL:
```txt
https://target-website.com/account?id=123
```
The above is an example of an Insecure Direct Object Reference (IDOR) vulnerability.
## Horizontal to Vertical Privilege Escalation
Often, a horizontal privilege escalation attack can be turned into a vertical privilege escalation, by compromising a more privileged user. For example, a horizontal escalation might allow an attacker to reset or capture the password belonging to another user, if the target user is an admin user, the attacker can gain admin access and perform vertical privilege escalation.
## Insecure Direct Object Reference
Also known as IDOR, is a type of vulnerability that arises where user-controlled parameter values are used to access resources or functions directly.

In some applications, the exploitable parameter does not have a predictable value, instead of an incrementing number, an application might use globally unique identifier (GUIDs) to identify users. This may prevent an attacker from guessing or predicting another user's identifier, however, GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced.
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
## Unprotected Functionality with Unpredictable URL
In some cases, sensitive functionality is concealed by giving it a less predictable URL. This is an example of so-called "security by obscurity". However, hiding sensitive functionality does not provide effective access control because users might still discover the obfuscated URL in a number of ways. Take the following URL as an example:
```txt
https://target-website.com/admin-panel-ybb86
```
This might not be easily guessable by an attacker. However, the application might still leak the URL, such as via JavaScript that constructs the user interface based on user's role:
```js
var isAdmin = false

if (isAdmin) {
	...
	var adminPanelURL = document.createElement('a')
	adminPanelURL.setAttribute('https://target-website.com/admin-panel-ybb86')
	adminPanelURL.innerText = 'Admin Panel'
}
```
The script above adds a link to the user's UI if they are an admin user. However, the script containing the URL is visible to everyone regardless of their role.
## Parameter-based Access Control Methods
Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location such as:
- Hidden HTML field
- Preset query string parameter
- Cookie

The application makes access control decision based on submitted value, for example:
```txt
https://target-website.com/login/home.php?admin=true
```
```txt
https://target-website.com/login.jsp?roleId=1
```
This approach is insecure because a user can modify the value and access functionalities they're not authorized to.