Using OWASP ZAP.
## Create or Modify Scanning Policies in ZAP
1. Go to **Analyse** in the menu, then select **Scan Policy Manager**.
2. Click **Add** button to create a new scan policy.
3. Adjust **Threshold** and **Strength** as necessary (see below for explanation).
4. Go through each policy and turn on/off each tests as necessary.

**Threshold** - This parameter controls the verbosity of each category. Lower threshold means ZAP reports a vulnerability based on little information, this will produce more findings but risks having false positives. A higher threshold means ZAP will only report vulnerabilities with a high degree of certainty, this will produce less results, but are more likely confirmed, however it may also produce false negatives.

**Strength** - This parameter controls how many tests are run for each category. Higher strength levels are likely to report additional findings at the expense of increasing scanning times significantly.
## Dealing with Authenticated Scans
First things first, make sure to disable ZAP HUD from the menu bar. Some things will not work as expected if it is enabled.

To record authentication, click the **Record a New ZEST Script** button on the menu bar (the icon in the middle of lock and help icon).

Set the title of the script and choose **Authentication** as the **Type** and **Server side script** as the **Record Type**. Skip **Initial URL** field and on the **Prefix** field, select the target URL, and checkbox **Load on start** option.

Once **Start Recording** is clicked, every HTTP request that goes through ZAP proxy will be recorded as part of the script. Click the **Open Browser** button on the menu bar (the firefox logo).

Navigate to the target's authentication page and login using your credentials. Once logged in, stop recording by clicking the **Record a New ZEST Script** button again.

In order to test the recorded script, press the **Run** button on the **Script Console** tab. View **Zest Results** and confirm that the recorded script is running.
### Creating a Context
After authentication process is recorded, configure ZAP to use it by creating a context.

To create a new context, go to the **Sites** tab and right-click the base URL of the target application on your **Sites** tab and select **Include in Context -> New Context**.

This will automatically create a regex that matches any page on the web application. Click on **Authentication**, and select **Script-based Authentication** on authentication method dropdown. Be sure to click **Load** button to the right of the script's name.

Next, define at least one user in the Users section. By default, ZEST script embeds the user and password that was used during the recording. However, ZAP still needs a user to be defined, or it will just skip authentication altogether.

Click **Add** and define the username and password. Once done, re-spider the application once again and notice that auth-only URLs are now being spidered.
### Avoiding Logouts
To prevent ZAP from logging itself out, look for any files/scripts containing a logout and exclude it from the context. This can be done by right-clicking on the base URL of the target application and select **Exclude from Context**.

Additionally, its also possible to specify indicators for ZAP to identify if session is still active or not. This is easily done by selecting parts of a response that only appear when a user is logged in or logged out. Once selected, right-click on the selected text and choose **Flag as Context -> (Your Context Name): Authentication Logged-in/Logged-out indicator**.

Now that ZAP has patterns to identify if it is logged in correctly, choose a **Verification Strategy** to tell ZAP how to use the configured patterns properly.
## Dealing with API Scans
The endpoints of an API won't normally expose information about other endpoints, making the discovery process harder. Instead of spidering APIs, it's best to rely on the development team to give a precise specification of the available endpoints and parameters in an API.

ZAP can import APIs defined by **OpenAPI** (formerly **Swagger**), **SOAP** or **GraphQL**. ZAP supports two methods to import API definitions: an offline file or a URL from where to download them. This can be done by selecting **Import -> Import an OpenAPI definition from a URL**.
## Integrating with CI/CD Pipelines
Having DAST added to the development process may sound pretty straightforward, but there are some caveats to it:

- We must decide at which stages of the development process we will run scans.
- We must decide what will trigger a scan. We can run scans on each commit made to code or on a scheduled basis.
- We must determine the intensity of each scan. Doing a full vulnerability scan on a medium-sized application will require significant time, and we don't want to slow down the development team.

Since no solution fits all scenarios, determining all of this must be done with the help of the development team so that security requirements are met without actually creating significant disturbances to their established processes.