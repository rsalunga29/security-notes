Also known as IDOR, is a type of access control vulnerability that arises when a web application exposes a direct reference to an object, like a file or a database resource, which the end-user can directly control to obtain access to other similar objects. If any user can access any resource due to the lack of a solid access control system, the system is considered to be vulnerable.

For example, if a user requests access to a file, they may get the following link:
```txt
http://target-website.com/file/download.php?file_id=1234
```
As we can see, the link directly references the file with (`file_id=1234`), if the web application does not have a proper access control mechanism in the back-end, we may be able to access any file by sending a request with a modified `file_id` parameter.

In many cases, we may find that the parameter values are easily guessable. However, in some applications, the exploitable parameter does not have a predictable value, instead of an incrementing number, an application might use globally unique identifier (GUIDs) to identify resources. This may prevent an attacker from guessing or predicting another user's identifier, however, GUIDs belonging to other resource might be disclosed elsewhere in the application where the resource is also referenced.

IDOR vulnerabilities are caused by a weak or improperly implemented access control system, and are most commonly association with horizontal privilege escalation, but they can also arise in relation to vertical privilege escalation. Other possibilities include exploiting password leakage or modifying parameters once the attacker has landed in the user's accounts page, for example.