XSS in hidden inputs is frequently very difficult to exploit because typical JavaScript events like `onmouseover` and `onfocus` can't be triggered due to the element being visible. However, this can still be done by using the `accessKey` attribute, which is a global attribute that specified a shortcut key to activate/focus an element. For example:
```html
<a href="https://www.sample-website.com" accesskey="c">Sample Website</a>
```
Depending on the user's browser, if they have triggered the access key, it will automatically activate the anchor tag and lead the user to the designated website.

*Note: The way of accessing the shortcut key is varying in different browsers:*

|Browser|Windows|Linux|Mac|
|---|---|---|---|
|Internet Explorer|[Alt] + _accesskey_|N/A||
|Chrome|[Alt] + _accesskey_|[Alt] + _accesskey_|[Control] [Alt] + _accesskey_|
|Firefox|[Alt] [Shift] + _accesskey_|[Alt] [Shift] + _accesskey_|[Control] [Alt] + _accesskey_|
|Safari|[Alt] + _accesskey_|N/A|[Control] [Alt] + _accesskey_|
|Opera|Opera 15 or newer: [Alt] + _accesskey  <br>_Opera 12.1 or older: [Shift] [Esc] + _accesskey_|   |   |

Provided that an attacker can persuade a victim into pressing the key combination, XSS can be executed inside a hidden attribute. For example:
```html
<input type="hidden" name="userId" accesskey="X" onclick="alert(1)">
```
However, if the reflection is repeated then the key combination will fail. A good workaround is to then inject another attribute that breaks the second reflection (i.e `" accessKey="X" onclick="alert(document.domain)" x='`).