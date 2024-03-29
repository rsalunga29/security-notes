Server-side template injection (SSTI) is when an attacker is able to use native template syntax to inject a malicious payload into a template, which is then executed server-side.

Template engines read tokenized strings from template documents and produce rendered strings with actual values in the output document. Templates are commonly used as an intermediary format by web developers to create dynamic website content.

Server-side template injection vulnerabilities arise when user input is concatenated into templates rather than being passed in as data. See following example:

**SSTI Non-Vulnerable Code**
```twig
$output = $twig->render("Dear {first_name},", array("first_name" => $user.first_name) );
```
> Note: This is not vulnerable to server-side template injection because the user's first name is merely passed into the template as data.

**SSTI Vulnerable Code**
```html
$output = $twig->render("Dear " . $_GET['name']);
```
> Note: In this example, instead of a static value being passed into the template, part of the template itself is being dynamically generated using the `GET` parameter `name`. As template syntax is evaluated server-side, this potentially allows an attacker to place a server-side template injection payload inside the `name` parameter

Aside from manual process, we can use [SSTImap](https://github.com/vladko312/SSTImap) or [tplmap](https://github.com/epinna/tplmap) to automate the detection and exploitation of SSTI vulnerabilities.