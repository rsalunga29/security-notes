The easiest way to detect injections is to supply mathematical expressions in curly brackets, for example:
```txt
http://target-website.com/?username={7*7}
http://target-website.com/?username=${7*7}
http://target-website.com/?username=#{7*7}
http://target-website.com/?username=%{7*7}
http://target-website.com/?username={{7*7}}
```
We will then look for the "49" in the response when injecting these payloads to identify that server-side evaluation occurred.