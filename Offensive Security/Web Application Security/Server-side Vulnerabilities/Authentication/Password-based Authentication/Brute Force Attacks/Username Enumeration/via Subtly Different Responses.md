Reset forms are often less well protected than login ones. Therefore, they very often leak information about a valid or invalid username. 

An application that replies with a "You should receive a message shortly" when a valid username has been found and "Username unknown, check your data" for an invalid entry leaks the presence of registered users.

Some web applications also leave the input field pre-filled with the (probably) valid username, so it is important to check for these subtle changes.

To automate this using Burp, follow the following steps:
1. Submit an invalid username and password. Highlight the `username` parameter in the request and send it to Burp Intruder.
2. On the **Payloads** tab, select "Simple List" and add the username wordlist.
3. On the **Settings** tab, under **Grep - Extract**, click **Add**. In the dialog that appears, scroll down through the response until you find the error message, highlight the text content of the message then the other settings will be automatically adjusted. Click **OK** and then start the attack.
4. When the attack is finished, notice that there is an additional column containing the error message you extracted. Sort the results using this column and find for any changes in the responses.