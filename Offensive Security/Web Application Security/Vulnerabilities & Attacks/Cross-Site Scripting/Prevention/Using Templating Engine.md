Many modern websites use server-side template engines such as Twig and Freemarker to embed dynamic content in HTML. These typically define their own escaping system. For example, in Twig, you can use the `e()` filter, with an argument defining the context:
```twig
{{ user.firstname | e('html') }}
```

Some other template engines, such as Jinja and React, escape dynamic content by default which effectively prevents most occurrences of XSS.