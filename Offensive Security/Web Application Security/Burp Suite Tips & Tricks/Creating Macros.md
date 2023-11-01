The **Macros** settings enable an attacker to create and manage macros that Burp can use during testing.

A macro is a predefined sequence of one or more requests. You can use macros within session handling rules to perform various task, such as:
- Fetching a page of the application (such as the user's home page) to check that the current session is still valid.
- Performing a login to obtain a new valid session.
- Obtaining a token or nonce to use as a parameter in another request.
- When you scan or fuzz a request in a multi-step process, a macro can perform any requests necessary to get the application into a state where the targeted request is accepted.
- In a multi-step process, a macro can complete the remaining steps of the process after the "attack" request. It can confirm the action was performed, or otherwise conclude the process.

As well as a sequence of requests, each macro specifies how cookies and parameters in the sequence should be handled, and any interdependencies between items.

You can add a new macro by following these steps:
1. In Burp, go to **Settings > Sessions**. Scroll down and look for **Macros**. Click **Add**, and in the dialog, select the requests you wish to include, and click **OK**.
2. Click **Test macro**, to make sure it is working as intended. Click **OK** once done.
3. In the **Session handling rules**, click **Add**, and in the dialog, click **Add** in the **Rule actions** then select **Run a macro**.
4. In the dialog, select the macro you have created and click **Add** then update any settings depending on your desired results.