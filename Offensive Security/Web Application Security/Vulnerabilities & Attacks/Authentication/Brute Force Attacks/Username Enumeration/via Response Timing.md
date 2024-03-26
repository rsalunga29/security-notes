Some authentication functions may contain flaws by design. One example is an authentication function where the username and password are checked sequentially. Imagine the following function:
```php
<?php

...[TRIM]...

$result = $db->query('SELECT * FROM users WHERE username="'.safesql($_POST['user']).'" AND active=1');

// $db->query() replies True if there are at least a row (so a user), and False if there are no rows (so no users)
if ($result) {
  // retrieve a row. don't use this code if multiple rows are expected
  $row = mysqli_fetch_row($result);

  // hash password using custom algorithm
  $cpass = hash_password($_POST['password']);
  
  // check if received password matches with one stored in the database
  if ($cpass === $row['cpassword']) {
	echo "Welcome $row['username']";
  } else {
    echo "Invalid credentials.";
  } 
} else {
  echo "Invalid credentials.";
}
```

First the code snippet executes a query to retrieve an entire row where the username matches the user input. If there are not results, it will return a generic error message. Otherwise, the provided password is hashed and compared, If the hashing algorithm used is strong enough, timing differences between the two conditions will be noticeable. By calculating `$cpass` using a generic `hash_password()` function, the response time will be higher than the other case. This small error could be avoided by checking user and password in the same step, having a similar time for both valid and invalid usernames.

Given that there could be a network glitch, it is easy to identify a valid user because it took way more time than other tested users. If the algorithm used was a fast one, time differences would be smaller, and an attacker could have a false positive because of a network delay or CPU load. However, the attack is still possible by repeating a large number of requests to create a model.

To automate this using Burp, follow the following steps:
1. Submit an invalid username and password. Highlight the `username` parameter in the request and send it to Burp Intruder.
2. On the **Payloads** tab, select "Simple List" and add the username wordlist.
3. During the attack, look for **Columns** menu on the attack modal, click it and select "Response received" and "Response completed" to see the time it takes for the server to response.
4. When the attack is finished, sort the results using these columns and look for any deviations.