## Access Gates
Also known as gates or checkpoints, these serves as "stages" within the software development pipeline. They ensure that code progresses through the pipeline only after meeting predefined quality and security criteria. It provides the following advantages:
1. **Enhanced Control**: Access gates provide checkpoints in the pipeline, allowing controlled progression to different stages.
2. **Quality Control**: Gates ensures that code meets predefined quality standards before advancing.
3. **Security Checks**: Gates enables security assessments, such as vulnerability scans, before deployment

There are multiple steps to implement these access gates, including:
1. **Manual Approvals**: Require manual approval before moving to the next stage, ensuring thorough reviews.
2. **Automated Tests**: Set up automated testing gates for code quality, unit tests, integration tests, etc.
3. **Security Scans**: Integrate security scanning tools to detect vulnerabilities in the codebase.
4. **Release Gates**: Use gates to verify proper documentation, versioning, and compliance.
5. **Environment Validation**: Validate the target environment's readiness before deployment.
6. **Rollback Plan**: Include a gate for a well-defined rollback plan in case of issues post-deployment.
7. **Monitoring**: Implement monitoring gates to assess post-deployment performance.
8. **Parallel Gates**: Run gates in parallel to expedite the pipeline without compromising quality.
9. **Auditing**: Regularly review gate configurations and results to ensure effectiveness.
## Two-Person Rule
The two-person rule is a concept in which a single person can't perform critical operations or pass "checks" all on their own. In CI/CD security context, enforcing this technical control ensures that in the event that a developer gets compromised, a build cannot be pushed through since it requires approval from another person.
## How to Secure the Pipeline
### Limit Branch Access
Restrict who can push to the main branch. Only trusted developers should have the ability to push code to this branch.
### Review Merge Requests
Enforce merge requests (or pull requests) to make main branch changes. Merge requests provide a way to review and approve code changes before merging. You can configure a merge request approvals to ensure multiple team members review and approve changes.
### Utilize CI/CD Variables
Avoid storing sensitive information directly in the source code. Instead, use environment variables or GitLab CI/CD variables (if using GitLab) to store secrets like API keys, passwords, and tokens. These variables can be protected and restricted to specific branches and tags.
### Limit Runner Access
Only allow trusted runners to execute CI/CD jobs. By specifying tags, you can register runners with specific tags and then restrict which runners can be used for jobs in CI/CD `.yaml` file. Only runners with the appropriate tags can run jobs on the main branch.
### Regular Audits
Conduct regular security reviews of the CI/CD configuration and pipeline. Review who has access and permissions and ensure that best practices are followed.
### Monitor and Alert
Set up monitoring and alerting for your pipeline. Implement security monitoring solutions to detect unusual or unauthorized activities in your environment and CI/CD pipeline.