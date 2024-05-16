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

This will automatically create a regex that matches any page on the web application. Click on **Authentication**, and select Script-based Authentication on