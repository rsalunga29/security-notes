Allowing users to upload file is commonplace and doesn't have to be dangerous as long as you take the right precautions. The most effective way to protect an application from file upload vulnerabilities are by following these best practices:
- Check the file extension against a whitelist of permitted extensions rather than a blacklist of prohibited ones. It's much easier to guess which extensions you might want to allow than it is to guess which ones an attacker might try to upload.
- Make sure the filename doesn't contain any substrings that may be interpreted as a directory or a traversal sequence (`../`).
- Rename uploaded files to avoid collisions that may cause existing files to be overwritten.
- Do not upload files to the server's permanent filesystem until they have been fully validated.
- As much as possible, use an established framework for preprocessing file uploads rather than attempting to write your own validation mechanisms.
- Randomize the names of the uploaded files in storage and store their sanitized filenames in a database.
- Limit file size and scan the uploaded files for malware and malicious strings.
- Utilize a web application firewall (WAF) as a secondary layer of protection.
- Disable specific functions that allows system commands to be executed through the web application (i.e for PHP, use `disable_functions` in `php.ini`).

Another thing that should be avoided it disclosing the uploads directory or providing direct access to the uploaded file. It is always recommended to hide the uploads directory from the end-users and only allow them to download the uploaded files through a download page.

If a download page is utilized, it is important to make sure that the page only grants access to files owned by the users (to avoid IDOR/LFI vulnerabilities) and that the users do not have acccess to the uploads directory. This can be achieved by utilizing the `Content-Disposition` and `nosniff` headers and using an accurate `Content-Type` header.