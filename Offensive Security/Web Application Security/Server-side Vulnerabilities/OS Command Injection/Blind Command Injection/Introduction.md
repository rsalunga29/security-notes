Many instances of OS command injection are blind vulnerabilities, which means the application does not return the output of the command via HTTP response. However, this can still be exploited using different techniques.

Imagine an application that lets users submit feedback about the site. The user enters their email address and feedback message. The application then calls out a `mail` program with the submitted details:
```bash
mail -s "great website" aFrom:peter@normal-user.net feedback@target-website.com
```
The output will not be returned to the application or the user. So using the `echo` payload won't work here.