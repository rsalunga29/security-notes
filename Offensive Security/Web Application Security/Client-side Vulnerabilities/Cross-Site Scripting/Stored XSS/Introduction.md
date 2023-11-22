Also known as second-order or persistent XSS. It arises when an application receives a malicious code, failing to validate it and permanently stores it in the application's database, which will then be executed when the application returns legitimate data including the malicious payload to the client.

For example, suppose a website allows users to submit comments on a blog posts with the following HTTP request:
```http
POST /post/comment HTTP/1.1
Host: vulnerable-website.com
Content-Length: 100

postId=3&comment=This+post+was+extremely+helpful.&name=Carlos+Montoya&email=carlos%40normal-user.net
```
After this comment is submitted, any user who visits the blog post will receive the following within the HTTP response:
```html
<p>This post was extremely helpful.</p>
```
Assuming the application doesn't perform any other processing of the data, an attacker can construct an attack like this:
```http
POST /post/comment HTTP/1.1
Host: vulnerable-website.com
Content-Length: 100

postId=3&comment=%3Cscript%3Ealert%28document.domain%29%3C%2Fscript%3E&name=Carlos+Montoya&email=carlos%40normal-user.net
```
Any user who visits the blog post will trigger the malicious code and open an alert popup containing the website's domain.