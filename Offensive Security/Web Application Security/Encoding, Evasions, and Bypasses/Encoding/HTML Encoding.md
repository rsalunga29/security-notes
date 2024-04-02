Documents transmitted via HTTP can send a charset parameter in the header to specify the character encoding of the document sent. This is the HTTP header: **Content-Type**:
```http
Content-Type:text/html;charset=utf-8
```

The following is an example of how character encoding using HTTP is done with different languages:

**PHP**
```php
header('Content-Type:text/html;charset=utf-8')
```
**ASP.Net**
```asp
<%Response.charset="utf-8"%>
```
**JSP**
```jsp
<%@ page contentType="text/html; charset=UTF-8"%>
```
**Meta HTML tag**
```html
<meta http-equiv="Content-Type" Content="text/html;charset=utf-8">
<meta charset="utf-8">
```