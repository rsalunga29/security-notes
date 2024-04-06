Often, security mechanisms choose to sanitize potential XSS vectors instead of blocking the entire request. For example, the most common is to HTML-encode common key characters, such as `<` (`&lt;`) and `>` (`&gt;`).
## String Manipulations
In some situations, a filter may manipulate payloads by removing malicious keywords. For example, removing `<script>` tags.

