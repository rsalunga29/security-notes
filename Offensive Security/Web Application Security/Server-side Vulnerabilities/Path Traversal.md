Also known as directory traversal, is a vulnerability that enables an attacker to read arbitrary files on the server that is running an application. This might include:
- Application code and data
- Credentials for back-end systems
- Sensitive operating system files
In some cases, an attacker might be able to write to arbitrary files, allowing them to modify application data or behavior, and ultimately take full control of the server.
## Reading arbitrary files via path traversal
Imagine a web application that displays images of products for sale. It loads the images using the following HTML:
```html
<img src="/loadImage?filename=218.png" />
```
The `loadImage` URL takes a `filename` parameter and returns the contents of the specified file by appending the value of the parameter to the base directory `/var/www/html/images` and uses a filesystem API to read the contents of the file. In other words, the application reads the following: `/var/www/html/images/218.png`.

Without proper defenses against path traversal attacks, an attacker can manipulate the requested URL to retrieve `/etc/passwd` file on the server by doing the replacing the `filename` parameter value to `https://target-website.com/loadImage?filename=../../../etc/passwd` which causes the application to return the following file path `/var/www/html/images/../../../etc/passwd`.

The `/etc/passwd` is a standard file in Unix-based operating systems that contains details of users registered on the server. On Windows, these details are stored on `Windows/win.ini`.

The sequence `../` is valid within a file path, and means step up one level in the directory. While on Windows, both `..\` and `../` are valid directory traversal sequences.