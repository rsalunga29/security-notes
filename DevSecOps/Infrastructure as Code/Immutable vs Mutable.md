Immutable vs mutable infrastructure refers to whether or not changes can be made to an infrastructure.
## Immutable
Immutable infrastructure means you cannot make changes to it. Once an infrastructure has been provisioned, that’s how it will be until it’s destroyed. So if we want to deploy the new version 2 of a web application, new resources will be provisioned to host the version 2, the version 1 infrastructure can be torn down after a successful deployment.

This approach has some drawbacks, as having multiple infrastructures stood up side by side or retrying on failed attempts is more resource-intensive than simply updating in place, but it allows for consistency across servers.

Example of immutable IaC tools are: Terraform, AWS CloudFormation, Google Cloud Deployment Manager, and Pulumi.
## Mutable
Mutable infrastructure means you can make changes to that infrastructure in place. The advantage here is that no additional resources need to be provisioned for this update, with the resources already being used just needing to be changed.

Where mutable infrastructure starts presenting issues is, imagine your web application update contains three changes, and whilst these updates are being made, one of the changes fails to apply. This means that we now have a web application version with two of the three changes required to be version 2. In other words, it’s no longer version 1 anymore but not quite version 2 either.

Example of mutable IaC tools are: Ansible, Chef, and Puppet.
## Choosing Between the Two
Choosing between mutable and immutable will entirely depend on the use case. Imagine the server instead is a critical database system that requires regular maintenance updates and patching. If you were to use an immutable infrastructure for this, the critical database would have to be rebuilt from scratch every time, which can be a risky process when dealing with business-critical data. So, in this instance, it might make sense to use a mutable infrastructure.