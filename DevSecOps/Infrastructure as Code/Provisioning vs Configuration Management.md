Considering what a tool's purpose is and when it is used in the development of infrastructure will tell us whether it is a "provisioning" tool or a "configuration management" tool.

To determine which tool falls into which category, we simply need to ask "what can it do?". If we think about four key tasks:
1. **Infrastructure Provisioning**: The setup of the infrastructure
2. **Infrastructure Management**: Changes made to the infrastructure
3. **Software Installation**: Initial installation and configuration of software/applications
4. **Software Management**: Updates made to software or config changes

There is no single tool that can perform all 4 of these tasks. Instead, combining two tools, a provisioning tool and a configuration management tool, is common practice to cover all these.

Provisioning tools are: Terraform, AWS CloudFormation, Google Cloud Deployment Manager, and Pulumi.

Configuration Management tools are: Ansible, Chef, Puppet, SaltStack.