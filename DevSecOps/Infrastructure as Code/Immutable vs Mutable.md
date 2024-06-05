Immutable vs mutable infrastructure refers to whether or not changes can be made to an infrastructure.
## Immutable
Immutable infrastructure means you cannot make changes to it. Once an infrastructure has been provisioned, that’s how it will be until it’s destroyed. So if we want to deploy the new version 2 of a web application, new resources will be provisioned to host the version 2, the version 1 infrastructure can be torn down after a successful deployment.
## Mutable
Mutable infrastructure means you can make changes to that infrastructure in place. The advantage here is that no additional resources need to be provisioned for this update, with the resources already being used just needing to be changed.

Where mutable infrastructure starts presenting issues is, imagine your web application update contains three changes, and whilst these updates are being made, one of the changes fails to apply. This means that we now have a web application version with two of the three changes required to be version 2. In other words, it’s no longer version 1 anymore but not quite version 2 either.

Example of mutable IaC tools are: Ansible, Chef, and Puppet.