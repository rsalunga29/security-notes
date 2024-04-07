These filters try to protect users from XSS attacks but, they do not cover all possible XSS attack scenarios and only focuses on Reflected-type XSS.

One of the most common Reflected XSS vectors is the following, and it is detected by all main filters:
```html
<svg/onload=alert(1)>
```

Removing the final greater-than sign, we have a bypass for browsers running XSS Auditor.