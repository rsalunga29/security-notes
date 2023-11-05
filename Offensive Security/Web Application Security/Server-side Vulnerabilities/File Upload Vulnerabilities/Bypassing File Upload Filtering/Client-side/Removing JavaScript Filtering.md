Some websites, uses client-side JavaScript to filter the file type a user is allowed to upload. However, this doesn't work as an attacker can modify the JavaScript to bypass its filtering.

In this example, we see a basic JavaScript function that checks the MIME types of the file about to be uploaded:
![[remove-js-1.png]]
We will use Burp Suite to remove the JavaScript function and upload a different file.
1. Using Burp Proxy, intercept the request. Right-click and select **Do intercept** then **Response to this request**.
2. Click **Forward** to see the response, this gives us the ability to modify the HTML of the respo