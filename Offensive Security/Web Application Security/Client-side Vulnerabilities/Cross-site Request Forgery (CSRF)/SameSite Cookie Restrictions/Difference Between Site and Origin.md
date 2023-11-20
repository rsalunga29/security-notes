The difference between site and origin is their scope. A site encompasses multiple domain names, whereas an origin only includes one. For example:

|   |   |   |   |
|---|---|---|---|
|**Request from**|**Request to**|**Same-site?**|**Same-origin?**|
|`https://example.com`|`https://example.com`|Yes|Yes|
|`https://app.example.com`|`https://intranet.example.com`|Yes|No: mismatched domain name|
|`https://example.com`|`https://example.com:8080`|Yes|No: mismatched port|
|`https://example.com`|`https://example.co.uk`|No: mismatched eTLD|No: mismatched domain name|
|`https://example.com`|`http://example.com`|No: mismatched scheme|No: mismatched scheme|

It is important to properly identify the difference between Same-site and Same-origin, as failure to do so can have serious security implications.