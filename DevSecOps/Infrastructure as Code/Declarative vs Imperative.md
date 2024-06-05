Below are the differences between declarative and imperative (also known as functional and procedural) IaC tools:
## Declarative
This approach involves declaring an explicit state for the infrastructure, min/max resources, x components, etc... The IaC tool will perform actions based on what is defined. In other words, it focuses on the what rather than the how.

Declarative IaCs are usually idempotent, which means the same result will be achieved when run repeatedly. This is because that check is done against the state file, and if the infrastructure is already provisioned, it will make no changes if rerun.

Declarative IaC is considered a more straightforward approach that is easier to manage, especially for long-term infrastructure.

IaC tools that are declarative are: Terraform, AWS CloudFormation, Pulumi, and Puppet.
## Imperative
This approach involves defining specific commands to be run to achieve the desired state. The commands needs to be executed in particular order.

Imperative IaCs are usually not idempotent, meaning if you run these tools multiple times, the same result won't be replicated or the tool may run into some configuration issues. This is because these commands will be run regardless of the state of your infrastructure, so running these commands on an already provisioned infrastructure may cause additional unwanted infrastructure to be added or may break the configuration of some existing components.

Imperative IaC is more flexible, giving the user more control and allowing them to specify exactly how the infrastructure is provisioned/managed rather than the tool itself taking care of it.

Example of imperative IaC tools are: Chef, SaltStack, and Ansible.
