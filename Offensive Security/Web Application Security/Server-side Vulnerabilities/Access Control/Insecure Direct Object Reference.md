Also known as IDOR, is a type of vulnerability that arises where user-controlled parameter values are used to access resources or functions directly.

In some applications, the exploitable parameter does not have a predictable value, instead of an incrementing number, an application might use globally unique identifier (GUIDs) to identify users. This may prevent an attacker from guessing or predicting another user's identifier, however, GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced.
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