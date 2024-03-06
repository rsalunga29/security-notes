Instead of implicitly trusting the `Content-Type` HTTP header, most secure websites try to verify the contents of the file or the specific sequence of bytes in the file's header or footer.

In cases of an image upload function, some applications might try to verify certain properties of an image, such as its dimensions. So if an attacker is trying to upload a PHP script, which doesn't have dimensions, the application can recognize this and reject the upload accordingly.

In other cases, an application might try to verify a file's magic bytes - which is a sequence of bytes in a file's header of footer used as a fingerprint or signature to determine whether the file contents match the expected file type. For example, JPEG files always begin with the bytes `FF D8 FF`. An attacker can use `hexedit` to modify the file's magic bytes based on a [public list](https://en.wikipedia.org/wiki/List_of_file_signatures) of file signatures.

However, even the most robust way of validating a file isn't foolproof. Special tools such as `ExifTool`, can be used to create polyglot JPEG file containing malicious code within its metadata. For example:
```nix
exiftool -Comment="<?php echo 'START ' . file_get_contents('/etc/passwd') . ' END'; ?>" image.jpg -o polyglot.php
```