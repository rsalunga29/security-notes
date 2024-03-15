The `HTTP` protocol works by accepting various HTTP methods as `verbs` at the beginning of an HTTP request. Depending on the web server configuration, web applications may be scripted to accept certain HTTP methods for their various functionalities and perform a particular action based on the type of the request.

While both `GET` and `POST` are the two most commonly used HTTP methods, any client can send any other methods in their HTTP requests and then see how the web server handles these methods. There are 9 different verbs that can be accepted as HTTP methods by web servers, other than the usual `GET ` and `POST`, the following are the rest:

| **Verb**  | **Description**                                                                                     |
| --------- | --------------------------------------------------------------------------------------------------- |
| `HEAD`    | Identical to a GET request, but its response only contains the `headers`, without the response body |
| `PUT`     | Writes the request payload to the specified location                                                |
| `DELETE`  | Deletes the resource at the specified location                                                      |
| `OPTIONS` | Shows different options accepted by a web server, like accepted HTTP verbs                          |
| `PATCH`   | Apply partial modifications to the resource at the specified location                               |

HTTP Verb Tampering is an attack in which an attacker takes advantage of a misconfiguration in web servers or web applications when handling different HTTP verbs/methods, to gain access to sensitive pages or even bypass certain security controls.

For example, imagine a web application and a web server are configured to only accept `GET` and `POST` methods, sending different HTTP methods would cause the application to show an error page, that itself isn't a vulnerability. However, if the web server configurations are not restricted to accept only `GET` and `POST` methods, and the web application is not developed to handle other types of HTTP requests, an attacker may be able to take advantage of this misconfiguration to gain access to admin/staff-only functionalities, or even bypass certain security controls.

As mentioned in the example above, exploiting HTTP Verb Tampering vulnerabilities is usually a relatively straightforward process. We just need to try alternate HTTP methods to see how they are handled by the web server and the web application.

Finally, what makes HTTP Verb Tampering attacks more common (and hence more critical), is that they are caused by a misconfiguration in either the back-end web server or the web application, either of which can cause the vulnerability.