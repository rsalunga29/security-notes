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
The `loadImage` URL takes a `filename` parameter and returns the contents of the specified file by appending the value