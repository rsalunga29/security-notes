Document Object Model (DOM) based XSS arises when JavaScript takes data from an attacker-controllable source and passes it to a sink that supports dynamic code execution, which enables attackers to execute malicious JavaScript including ones that allows them to hijack other user's accounts.

The most common source for DOM XSS is the URL, which is typically accessed with the `window.location` object. An attacker can construct a link to send a victim to a vulnerable page with payload in the query string and fragment portions of the URL.

The following are some of the main sinks that can lead to DOM-XSS vulnerabilities:
- `document.write()`
- `document.writeln()`
- `document.domain`
- `element.innerHTML`
- `element.outerHTML`
- `element.insertAdjacentHTML`
- `element.onevent`

<!-- @TODO: Transfer Sources and Sinks to DOM-based vulnerabilities -->
## Sources
A source is a JavaScript property that accepts data that is potentially attacker-controlled. The `location.search` property is a good example of a source that an attacker can easily control, since it reads input from the URL query string. Ultimately, any property that an attacker can control is a potential source.
## Sinks
A sink is a potentially dangerous JavaScript function or DOM object that can cause undesirable effect if malicious data is passed to it. An example of a HTML sink is `document.body.innerHTML` since it allows an attacker to inject malicious HTML and execute arbitrary JavaScript. Another example is the `eval()` function because it processes the argument that is passed into it as JavaScript.