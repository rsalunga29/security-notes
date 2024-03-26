The most common place to identify a potential IDOR vulnerability is through URL and API parameters. Whenever we receive a specific file or resource, we should study the HTTP requests to look for URL parameters or APIs with an object reference (e.g. `?uid=1` or `?filename=file_1.pdf`).

In most cases, the values are easily predictable by just incrementing the values. However, we can also try to fuzz the application to try thousands of variations and see if they return any data.

Another example, consider a website that uses the following URL to access the customer account page, by retrieving information from the back-end database:
```txt
https://insecure-website.com/customer_account?customer_number=132355
```
Here, the customer number is used directly as a record index in queries that are performed on the back-end database. If no other controls are in place, an attacker can simply modify the `customer_number` value, bypassing access controls to view the records of other customers. This is an example of an IDOR vulnerability leading to horizontal privilege escalation.

An attacker might be able to perform horizontal and vertical privilege escalation by altering the user to one with additional privileges while bypassing access controls.

Finally, these can also happen in static files. For example, a website might save chat message transcripts to disk using an incrementing filename, and allow users to retrieve these by visiting a URL like the following:
```txt
https://insecure-website.com/static/12144.txt
```
In this situation, an attacker can simply modify the filename to retrieve a transcript created by another user and potentially obtain user credentials and other sensitive data.