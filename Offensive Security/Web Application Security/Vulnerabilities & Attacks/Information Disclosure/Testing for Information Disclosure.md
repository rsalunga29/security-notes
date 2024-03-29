Sensitive data can be leaked in all kinds of places, so it is important to not develop "tunnel vision" during testing and miss anything that could be useful at a later time.

The following are some examples of high-level techniques and tools that you can use to help identify information disclosure vulnerabilities during testing.
## Fuzzing
If we identify an interesting parameter, we can try submitting unexpected data types and specially-crafted fuzz strings to see what effect this has. It is important to pay close attention, although responses sometimes disclose interesting information, they can also give hints on how the application behaves.

While this process can be done manually, is can also be automated which provides several benefits:
- Add payload positions to parameters and use pre-built wordlists of fuzz strings to test a high volume of different inputs in quick succession.
- Easily identify differences in responses by comparing HTTP status codes, response times, lengths, and so on.
- Use grep matching rules to quickly identify occurrences of keywords, such as `error`, `invalid`, `SELECT`, `SQL`, and so on.
- Apply grep extraction rules to extract and compare the content of interesting items within responses.

Alternatively, the [Logger++](https://portswigger.net/bappstore/470b7057b86f41c396a97903377f3d81) extension, available from the BApp store can also be used to extend the log filtering function of Burp Suite.
## Using Burp Scanner
[Burp Suite Professional](https://portswigger.net/burp/pro) users have the benefit of Burp Scanner. This provides live scanning features for auditing items while you browse, or you can schedule automated scans to crawl and audit the target site on your behalf. Burp Scanner will alert you if it finds sensitive information such as private keys, email addresses, and credit card numbers in a response. It will also identify any backup files, directory listings, and so on.
## Using Burp E