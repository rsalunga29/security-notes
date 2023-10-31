1. Submit an invalid username and password. Highlight the `username` parameter in the request and send it to Burp Intruder.
2. Experiment with different usernames and passwords. Pay particular attention to the response times. Notice that when the username is invalid, the response time is roughly the same. However, when you enter a valid username, the response time is increased depending on the length of the password you entered.
3. On the **Payloads** tab, select "Simple List" and add the username wordlist.
4. When the attack finishes, at the top of the dialog, click **Columns** and select the **Response received** and **Response completed** options. These two columns are now displayed in the results table.
5. With the correct username in hand, close the attack and go back to **Positions** and **Payloads** tab and set the correct settings to brute force for the password.
6. When successful, look for a `302` HTTP response code