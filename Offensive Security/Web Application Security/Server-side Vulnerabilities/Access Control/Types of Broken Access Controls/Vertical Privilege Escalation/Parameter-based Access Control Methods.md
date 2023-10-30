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