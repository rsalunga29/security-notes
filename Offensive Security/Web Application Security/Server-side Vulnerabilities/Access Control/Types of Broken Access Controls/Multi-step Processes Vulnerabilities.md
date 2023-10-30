Many website implement important functions over a series of steps. This is common when:
- A variety of inputs or options need to be capture
- The user needs to review and confirm details before the action is performed

For example, the administrative function to update user details might involve the following steps:
1. Load the form that contains the detail of a specific user
2. Submit the changes
3. Review the changes and confirm

Sometimes, a website will implement rigorous access controls over some of these steps, but ignore others. For example, access controls are properly applied to step 1 and step 2, but not to step 3. In this case, the website assumes that the user will only reach step 3 if they have completed the first two steps. However, an attacker can gain unauthorized access to the function by skipping the first two steps and directly submitting the request for the third step with required parameters.