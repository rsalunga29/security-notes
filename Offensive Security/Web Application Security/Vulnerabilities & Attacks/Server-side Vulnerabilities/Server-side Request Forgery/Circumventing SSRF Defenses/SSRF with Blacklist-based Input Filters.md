Some applications block input containing hostnames like `127.0.0.1` and `localhost`, or sensitive URLs like `/admin`. However, you can often circumvent the filter by using the following techniques:
- Using an alternative IP representation of `127.0.0.1`, such as `2130706433`, `017700000001`, or `127.1`.
- Register your own domain name that resolves to `127.0.0.1`. You can use `spoofed.burpcollaborator.net` for this purpose.
> Note: If Burp Collaborator is not available, we can use [CanaryTokens](https://canarytokens.org/generate#) and [interactsh](https://github.com/projectdiscovery/interactsh) as alternatives.
- Use URL encoding or case variation (aDmIn instead of admin) to obfuscate blocked strings.
- Using a URL that you control, which redirects to target URL. Trying using different redirect codes, as well as protocols for the target URL. For example, switching `http` to `https` during redirect has been shown to bypass some anti-SSRF filters.

Often times, multiple anti-SSRF filters are deployed, you can combine the techniques described above to bypass the filters and exploit the SSRF vulnerabilities.