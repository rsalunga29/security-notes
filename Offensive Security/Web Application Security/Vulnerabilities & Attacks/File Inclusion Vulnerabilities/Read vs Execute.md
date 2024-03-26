From our examples in [Introduction](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FIntroduction), we can see that File Inclusion vulnerability may occur in any web server and any development frameworks. The most important thing to keep in mind is that some of the functions only read the content of the specified files, while others may execute the specified files, which may lead to code executions.

The following table shows which functions may execute files and which only read file content.
> Note: Some functions do allow including remote URLs but do not allow code execution. In this case, we would still be able to exploit the vulnerability to enumerate local ports and web applications through SSRF.
## PHP
| **Function**                 | **Read Content** | **Execute** | **Remote URL** |
| ---------------------------- | :--------------: | :---------: | :------------: |
| `include()`/`include_once()` |        ✅         |      ✅      |       ✅        |
| `require()`/`require_once()` |        ✅         |      ✅      |       ❌        |
| `file_get_contents()`        |        ✅         |      ❌      |       ✅        |
| `fopen()`/`file()`           |        ✅         |      ❌      |       ❌        |
## NodeJS

| **Function**    | **Read Content** | **Execute** | **Remote URL** |
| --------------- | :--------------: | :---------: | :------------: |
| `fs.readFile()` |        ✅         |      ❌      |       ❌        |
| `fs.sendFile()` |        ✅         |      ❌      |       ❌        |
| `res.render()`  |        ✅         |      ✅      |       ❌        |
## Java

| **Function** | **Read Content** | **Execute** | **Remote URL** |
| ------------ | :--------------: | :---------: | :------------: |
| `include`    |        ✅         |      ❌      |       ❌        |
| `import`     |        ✅         |      ✅      |       ✅        |
## .NET
| **Function**            | **Read Content** | **Execute** | **Remote URL** |
| ----------------------- | :--------------: | :---------: | :------------: |
| `@Html.Partial()`       |        ✅         |      ❌      |       ❌        |
| `@Html.RemotePartial()` |        ✅         |      ❌      |       ✅        |
| `Response.WriteFile()`  |        ✅         |      ❌      |       ❌        |
| `include`               |        ✅         |      ✅      |       ✅        |