Reset forms are often less well protected than login ones. Therefore, they very often leak information about a valid or invalid username. Some web applications leave the input field pre-filled with the (probably) valid username, so it is important to check for these subtle changes.

While some may put a hidden field that may contain the wrong username, if the username is valid, this hidden input field will be empty, otherwise, it will include the value of the invalid username. It is a good idea to check the source code.

To automate this using Burp, follow the following steps:
1. Submit an invalid username and password. Highlight the `username` parameter in the request and send it to Burp Intruder.
2. On the **Payloads** tab, select "Simple List" and add the username wordlist.
3. On the **Settings** tab, under **Grep - Extract**, click **Add**. In the dialog that appears, scroll down through the response until you find the error message, highlight the text content of the message then the other settings will be automatically adjusted. Click **OK** and then start the attack.
4. When the attack is finished, notice that there is an additional column containing the error message you extracted. Sort the results using this column and find for any changes in the responses.