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
## Detection
The easiest way to detect injections is to supply mathematical expressions in curly brackets, for example:
```html
{7*7}
${7*7}
#{7*7}
%{7*7}
{{7*7}}
```
We will then look for the "49" in the response when injecting these payloads to identify that server-side evaluation occurred.

The most difficult way to identify SSTI is to fuzz the template by injecting combinations of special characters used in template expressions. These characters include `${{<%[%'"}}%\`. If an exception is caused, this means that we have some control over what the server interprets in terms of template expressions.

The diagram below helps us identify if we are dealing with an SSTI vulnerability and also to identify the templating engine.
![[ssti-diagram.png]]

In addition to the above diagram, we can try the following approaches to recognize the technology we are dealing with:
- Check verbose errors for technology names. Sometimes just copying the error in Google search can provide us with a straight answer regarding the underlying technology used
- Check for extensions. For example, `.jsp` extensions are associated with Java. When dealing with Java, we may be facing an expression language/OGNL injection vulnerability instead of traditional SSTI
- Send expressions with unclosed curly brackets to see if verbose errors are generated. Do not try this approach on production systems, as you may crash the webserver.