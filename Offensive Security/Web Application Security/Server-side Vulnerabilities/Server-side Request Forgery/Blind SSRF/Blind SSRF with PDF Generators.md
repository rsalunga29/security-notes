Some websites, allows their users to generate a PDF based on the input they have provided.
## Data Exfiltration with Blind SSRF
In the following example scenario, a website accepts a `.html` input via file upload, which then converts the said HTML file into a PDF.

1. First let's confirm 
## SSRF Chain with XSS
If these inputs are non-sanitized, this can lead to a SSRF by chaining it with a [Cross Site Scripting](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Site%20Scripting%2FIntroduction) (XSS) attack.

Usual pre-requisite for an attack like this is for the website to be vulnerable from Cross Site Scripting (XSS). For example, a target website generates an invoice that includes your full name in it. You can use the following payload as your full name: `<iframe src="http://attacker-website.com" width="400" height="400">` which then a PDF generator library would take and generate a PDF and executing the `iframe` code an attacker has provided.
