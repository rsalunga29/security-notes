One misconception is that users will always supply values for mandatory input fields. While browsers and client-side validation can prevent a user from submitting a form without all the mandatory inputs, attackers can tamper with the parameters in transit. **This even extends to removing parameters entirely**.

This usually happens in cases where multiple functions are implemented using the same backend script. For example, the presence or absence of the `currentPassword` parameter in the `/change-password` request URL can determine which code is executed, whether it will change the password or assign a new one entirely, as if the account is being newly registered.

When probing for logic flaws, developers must try removing each parameter in turn and observe what effect it has on the response:
- Only remove one parameter at a time to ensure all relevant code paths are reached.
- Try deleting the name of the parameter as well as the value. The server will typically handle both cases differently.
- Follow multi-stage processes through to completion. Sometimes tampering with a parameter in one step will have an effect on another step further along in the workflow.