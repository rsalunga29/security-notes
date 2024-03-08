A common file upload attack that uses a malicious string for the upload file name, which may get executed or processed if the uploaded file is displayed on the page.

For example, if we name a file `file$(whoami).jpg` or ``file`whoami`.jpg`` or `file.jpg||whoami`, and then the web application attempts to move the uploaded file with an OS command (e.g. `mv file /tmp`), then our file name would inject the `whoami` command, which would get executed, leading to remote code execution.

Similarly, we can also use a XSS payload in the file name (e.g `<script>alert(window.origin);</script>.jpg`)