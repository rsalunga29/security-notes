Document Object Model (DOM) based XSS arises when JavaScript takes data from an attacker-controllable source and passes it to a sink that supports dynamic code execution, which enables attackers to execute malicious JavaScript which typically allows them to hijack other user's accounts.
## Source
A source is a JavaScript property that accepts data that is potentially attacker-controlled. The `location.search` property is a good example of  a source that an attacker can easily control, since it reads input from the URL query string.
## Sinks