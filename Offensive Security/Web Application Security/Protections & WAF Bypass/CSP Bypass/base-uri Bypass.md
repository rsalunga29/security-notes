A dangling markup injection can be performed if the `base-uri` directive is absent in the defined CSP. Attackers can abuse the base tag to contain an XSS by making the page load a script from a server they control, if the script has a relative path (i.e `/js/app.js`). An HTTPS URL should be used if the vulnerable page is loaded over HTTPS.

In order for this to work 
