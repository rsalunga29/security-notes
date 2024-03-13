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