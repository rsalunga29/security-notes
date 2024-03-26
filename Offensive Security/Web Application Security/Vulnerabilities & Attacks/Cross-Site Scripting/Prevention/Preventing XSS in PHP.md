The `htmlentities` is a built-in function in PHP that is used to encode entities to escape user-supplied input when inside an HTML context. The function accepts three arguments:
- The input string
- A flag, for example `ENT_QUOTES` which specifies all quotes should be encoded
- The character set, which in most cases should be UTF-8

For example:
```php
<?php echo htmlentities($input, ENT_QUOTES, 'UTF-8'); ?>
```

Unfortunately in JavaScript contexts, PHP doesn't provide an API to Unicode-escape a string. You will be needing a custom code to do that.