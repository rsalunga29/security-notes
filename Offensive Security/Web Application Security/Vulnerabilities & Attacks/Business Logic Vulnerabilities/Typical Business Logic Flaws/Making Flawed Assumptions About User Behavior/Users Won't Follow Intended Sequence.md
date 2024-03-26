Many transactions rely on predefined workflows consisting of a sequence of steps. The web interface typically guide users through this process. However, attackers won't necessarily adhere to this intended sequence.

Making assumptions about the sequence of events can lead to dangerous flaws that may be relatively simple to exploit. An attacker can just use Burp Proxy to intercept the request, use Repeater to replay the request at will, and use forced browsing to perform any interactions with the functionality or server in any order they want.

To identify these kind of flaws, you should use forced browsing to submit requests in an unintended sequence. For example, you might skip certain steps, access a single step more than once, return to earlier steps, and so on. Although you can often just submit a `GET` or `POST` request to a specific URL, sometimes you can access steps by submitting different sets of parameters to the same URL.

<!-- @TODO: Link Information Disclosure from server-side vulnerabilities -->
This kind of testing will often cause the application to throw an exception because expected variables have null or uninitialized values. In this case, pay close attention to any error messages or debug information, as these can be a valuable source of information disclosure, which can be used to help fine-tune the attack.