1. Submit an invalid username and password. Highlight the `username` parameter in the request and send it to Burp Intruder.
2. On the **Payloads** tab, select "Simple List" and add the username wordlist.
3. On the **Settings** tab, under **Grep - Extract**, click **Add**. In the dialog that appears, scroll down through the response until you find the error message, highlight the text content of the message then the other settings will be automatically adjusted. Click **OK** and then start the attack.
4. When the attack is finished, notice that there is an additional column containing the error message you extracted. Sort the results using this column and find for any changes in the responses.
5. With the correct username in hand, close the attack and go back to **Positions** and **Payloads** tab and set the correct settings to brute force for the password.
6. When finished, look for a `302` HTTP response.