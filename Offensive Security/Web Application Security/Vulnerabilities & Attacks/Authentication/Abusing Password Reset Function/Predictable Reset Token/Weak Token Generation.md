Some applications create tokens using known or predictable values, such as local time or the username that requested the action and then hash or encode the value. This is bad security practice as tokens must be pure-random value and its encoding must not be easily reversible as it could allow an attacker to understand how a token is generated, allowing them to generate their own tokens.

Take for example this PHP code. It is the logical equivalent of the vulnerability reported as [CVE-2016-0783](https://www.cvedetails.com/cve/CVE-2016-0783/) on Apache OpenMeeting:
```php
<?php
function generate_reset_token($username) {
  $time = intval(microtime(true) * 1000);
  $token = md5($username . $time);
  return $token;
}
```
It's easy to spot the vulnerability in the code above, as any attacker that knows a valid username can get the server time by reading the `Date` header in the HTTP response. The attacker can then brute force the `$time` value in a matter of seconds and get a valid reset token.
> Note: Do bear in mind that any HTTP header can be stripped or altered by placing a reverse proxy in front of the application. However, there are various other ways to determine time, such as in sent or received in-app messages, an email header, or last login time, to name a few.