## Masking Variables
You can mask variables in your .gitlab-ci.yml file by using the CI_JOB_TOKEN predefined variable. This token is automatically set by GitLab and can be used to mask any variable value you want to keep hidden.

For example, if you have a variable named MY_SECRET_KEY, you can use it like this:
```yaml
my_job:
  script:
    - echo "$MY_SECRET_KEY" # This will expose the secret
    - echo "masked: $CI_JOB_TOKEN" # This will mask the secret
```
## Use Secure Variables
If you want to store secrets securely in GitLab, you can use GitLab CI/CD variables with the "Masked" option enabled. These variables are stored securely and are never exposed in job logs, even if you use them directly in your scripts. To create a secure variable:
- Go to the GitLab project.
- Navigate to Settings > CI/CD > Variables.
- Add a new variable, select the "Masked" checkbox, and provide the value.
- Once you've added a secure variable, you can use it in your `.gitlab-ci.yml` file without worrying about it being exposed in logs.
It is also important to ensure that the CI/CD scripts do not inadvertently echo or print sensitive information, even when using masked variables.
## Access Control
Limit access to CI/CD variables and logs. Only authorized can view job logs and variables. You can configure project-level and group-level access controls to achieve this.