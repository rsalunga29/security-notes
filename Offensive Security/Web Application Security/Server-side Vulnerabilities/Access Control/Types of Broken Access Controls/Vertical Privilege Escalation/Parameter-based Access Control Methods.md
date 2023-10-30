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
This vulnerability can also exist in JSON request/response, for example:
```txt
POST /my-account/change-email HTTP/2
Host: 0a63002d0312101e8010d5fd00d40081.web-security-academy.net
Cookie: session=X4A5Qj0ek0Ef0E3IN72JTvwPa4B6fM09
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: text/plain;charset=UTF-8
Content-Length: 33
Origin: https://0a63002d0312101e8010d5fd00d40081.web-security-academy.net
Referer: https://0a63002d0312101e8010d5fd00d40081.web-security-academy.net/my-account?id=wiener

{"email":"wiener@admin-user.net"}
```
```
HTTP/2 302 Found
Location: /my-account
Content-Type: application/json; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 125

{
  "username": "wiener",
  "email": "wiener@admin-user.net",
  "apikey": "cTknnffiylXSYu61HaLvWNn0FNXeF4ye",
  "roleid": 1
}
```
Seeing that `roleid` is given back as a response, we can assume that it can also accept it as a parameter for our HTTP request.

This approach is insecure because a user can modify the value and access functionalities they're not authorized to.