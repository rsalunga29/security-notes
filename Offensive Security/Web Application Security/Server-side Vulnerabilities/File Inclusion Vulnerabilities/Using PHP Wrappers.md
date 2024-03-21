Many popular web applications are developed in PHP, along with various custom web applications built with different PHP frameworks, like Laravel or Symfony. If we identify an LFI vulnerability in PHP web applications, then we can utilize different [PHP Wrappers](https://www.php.net/manual/en/wrappers.php.php) to be able to extend our LFI exploitation, and even potentially reach remote code execution.

PHP Wrappers allow us to access different I/O streams at the application level, including standard input/output, file descriptors, and memory streams.
## Input Filters
PHP Filters are a type of PHP wrappers,