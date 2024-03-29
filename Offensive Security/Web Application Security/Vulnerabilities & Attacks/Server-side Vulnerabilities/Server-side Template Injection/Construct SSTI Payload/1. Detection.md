The most straightforward way to identify SSTI is to fuzz the template by injecting combinations of special characters into the template and analyzing the difference in server responses. These characters include `${{<%[%'"}}%\`. If an exception is caused, this means that we have some control over what the server interprets in terms of template expressions.
## Plaintext Context
Most template languages allow you to freely input content either by using HTML tags directly or by using the template's native syntax, which will be rendered to HTML on the back-end before the HTTP response is sent.

One way to detect SSTI is to supply mathematical expressions in curly brackets, for example:
```txt
http://target-website.com/?username={7*7}
http://target-website.com/?username=${7*7}
http://target-website.com/?username=#{7*7}
http://target-website.com/?username=%{7*7}
http://target-website.com/?username={{7*7}}
http://taget-website.com/?username=<%=7*7%>
```
We will then look for the "49" in the response when injecting these payloads to identify that server-side evaluation occurred.
## Code Context
In other cases, the vulnerability is exposed by user input being placed within a template expression as parameter. For example:
```txt
greeting = getQueryParameter('greeting')
engine.render("Hello {{"+greeting+"}}", data)
```
On the website, the resulting URL would be something like:
```txt
http://vulnerable-website.com/?greeting=data.username
```
This would be rendered in the output to `Hello Carlos`, for example.

Most attackers miss this context during their assessments simply because it doesn't result in obvious XSS and is almost identical from a simple hashmap lookup. One method of testing for SSTI in this context is to make sure the parameter doesn't contain a direct XSS vulnerability:
```txt
http://target-website.com/?username=data.username<xss>
```
If the result is either blank output, encoded tags, or an error message, that means there is no XSS. The next step is to try to break out of the statement using common templating syntax and test for XSS again:
```txt
http://target-website.com/?username=data.username}}<xss>
```
If this again results in a blank output or an error message, it either means the syntax that was used is from the wrong templating engine or SSTI is not possible. Otherwise, if the output is rendered correctly along with the arbitrary HTML payload, it is a key indication that SSTI exists.