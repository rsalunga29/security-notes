First-order SQL injection occurs when the application processes user input from an HTTP request and incorporates the input into a SQL query in an unsafe way.

Second-order SQL injection also known as stored SQL injection, occurs when the application takes the malicious user input from an HTTP request and stores it in the database for future use, no vulnerability occurs at this point. Later, when handling a different HTTP request, the application retrieves the stored data containing the malicious input and incorporates it into a SQL query in an unsafe way.

Second-order SQL injection often occurs in situations where developers safely sanitizes user input before storing it in the database, but overlook potential vulnerabilities when processing the data. This oversight can lead to unsafe data handling leading to a SQL injection vulnerability.