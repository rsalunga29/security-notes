Many popular web applications are developed in PHP, along with various custom web applications built with different PHP frameworks, like Laravel or Symfony. If we identify an LFI vulnerability in PHP web applications, then we can utilize different [PHP Wrappers](https://www.php.net/manual/en/wrappers.php.php) to be able to extend our LFI exploitation, and even potentially reach remote code execution.

PHP Wrappers allow us to access different I/O streams at the application level, including standard input/output, file descriptors, and memory streams.
## Input Filters
PHP Filters are a type of PHP wrappers, where we can pass different types of inputs and have it filtered by the filter type we specify. We can access the PHP filter wrapper using `php://filter/`.

The filter wrapper has multiple parameters, but main ones required for an attack are `resource` and `read`. The `resource` parameter is required filter wrappers, and it is used to specify the stream we would like to apply the filter on, while the `read` parameter allows us to apply different filters on the input resource.

There are four different types of filters available for use, which are [String Filters](https://www.php.net/manual/en/filters.string.php), [Conversion Filters](https://www.php.net/manual/en/filters.convert.php), [Compression Filters](https://www.php.net/manual/en/filters.compression.php), and [Encryption Filters](https://www.php.net/manual/en/filters.encryption.php). However, the most important filter for LFI attacks is the `convert.base64-encode` filter under Conversion Filters.
## Source Code Disclosure
The first would be to fuzz for different available PHP pages using tools like `ffuf` or `GoBuster`. Once we have a list of potential PHP files we want to read, we can start disclosing their sources with the `base64` PHP filter. Let's try to read the source code of `config.php` using the base64 filter, by specifying `convert.base64-encode` for the `read` parameter and `config` for the `resource` parameter, as follows:
```url
http://target-website.com/?language=php://filter/read=convert.base64-encode/resource=config.php
```