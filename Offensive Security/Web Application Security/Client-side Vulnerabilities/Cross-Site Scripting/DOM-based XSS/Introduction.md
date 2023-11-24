Document Object Model (DOM) based XSS arises when JavaScript takes data from an attacker-controllable source and passes it to a sink that supports dynamic code execution, which enables attackers to execute malicious JavaScript including ones that allows them to hijack other user's accounts.
## Sources
A source is a JavaScript property that accepts data that is potentially attacker-controlled. The `location.search` property is a good example of a source that an attacker can easily control, since it reads input from the URL query string. Ultimately, any property that an attacker can control is a potential source.

The following are the typical sources that can be used to exploit DOM XSS:
- `document.URL`
- `document.documentURI`
- `document.URLUnencoded`
- `document.baseURI`
- `location`
- `document.cookie`
- `document.referrer`
- `window.name`
- `history.pushState`
- `history.replaceState`
- `localStorage`
- `sessionStorage`
- `IndexedDB (mozIndexedDB, webkitIndexedDB, msIndexedDB)`
- `Database`
## Sinks
A sink is a potentially dangerous JavaScript function or DOM object that can cause undesirable effect if malicious data is passed to it. An example of a HTML sink is `document.body.innerHTML` since it allows an attacker to inject malicious HTML and execute arbitrary JavaScript. Another example is the `eval()` function because it processes the argument that is passed into it as JavaScript.