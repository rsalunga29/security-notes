When trying to understand the high-level logic behind a reset form, it is unimportant if it sends a token, a temporary password, or requires the correct answer. At a high level, when a user inputs the expected value, the reset functionality lets the user change the password or pass the authentication phase.

While the function that checks if a token is valid or is the correct one for a given account is carefully developed with security in mind. It is sometimes vulnerable during the second phase of the process, when the user resets the password after the first login has been granted.

Imagine the following scenario. After creating an account of our own, we request a password reset.
![[username-injection.png]]
We can try to inject a different username and/or email address, looking for a possible hidden input value or guessing any valid input name.

It has been observed that some applications give precedence to received information against information stored in a session value. An example of vulnerable code looks like this (the `$_REQUEST` variable contains both `$_GET` and `$_POST`):
```php
<?php
  if isset($_REQUEST['userid']) {
	$userid = $_REQUEST['userid'];
  } else if isset($_SESSION['userid']) {
	$userid = $_SESSION['userid'];
  } else {
	die("unknown userid");
  }
```

Imagine a web application that allows admin or helpdesk employees to reset other user's passwords. Often, the function that changes the password is reused and shares the same codebase with the one used by standard users to change their password. For example, the following is the standard request that users use to change their password:
```http
POST /change-password.php HTTP/1.1
...

oldpassword=nots3cure&newpassword=s4f3rP@sS!&confirm=s4f3rP@sS!&submit=submit
```

If we tamper the request by adding a `userid` field, we can change the password for another user:
```http
POST /change-password.php HTTP/1.1
...

oldpassword=nots3cure&newpassword=s4f3rP@sS!&confirm=s4f3rP@sS!&userid=administratorsubmit=submit
```

To avoid this, an application must always check for authorization before performing any change.