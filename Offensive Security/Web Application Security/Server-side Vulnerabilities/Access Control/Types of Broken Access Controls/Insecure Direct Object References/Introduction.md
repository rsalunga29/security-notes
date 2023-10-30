Also known as IDOR, is a type of access control vulnerability that arises where user-controlled parameter values are used to access resources or functions directly.

In some applications, the exploitable parameter does not have a predictable value, instead of an incrementing number, an application might use globally unique identifier (GUIDs) to identify users. This may prevent an attacker from guessing or predicting another user's identifier, however, GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced.

IDOR vulnerabilities are most commonly association with horizontal privilege escalation, but they can also arise in relation to vertical privilege escalation.