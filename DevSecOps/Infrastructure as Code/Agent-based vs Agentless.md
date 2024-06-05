Agent-based vs Agentless is a term that extends beyond infrastructure as code and is also used in the context of monitoring and security tools. In the context of IaC:
## Agent-based
Agent-based IaC needs an "agent" to be installed on the server that is to be managed. It runs in the background and acts as a communication channel between the IaC tool and the resources that need managing. This agent is responsible or executing and reporting on the state of the infrastructure/managed resource.

An agent-based IaC tool can perform tasks even when the system has limited connectivity or is offline, making it a robust choice for automation. It is important to continuously monitor the agent software closely so that it can be restarted in the event of a crash.

Some agent-based IaC tools will also require opening ports on the server for inbound and outbound traffic, allowing the agent to push/pull configuration information.

Examples of agent-based IaC tools are: Puppet, Chef, and Saltstalk.
## Agentless
Agentless IaC tools do not require agents to be installed on the target systems. Instead, these tools leverage existing communication protocols such as SSH, WinRM or Cloud APIs to interact with the target system.

Agentless IaC tools benefit from being easier to use; their simplicity during set-up can mean faster deployment time, and their agentless nature can also mean the tool can be deployed across multiple environments without custom agent changes needing to be made based on each environment’s needs, making it a flexible choice. It also requires less maintenance.

The only downside of agentless IaC tools is that, they generally offer less control over target systems than agent-based tools.

Examples of agentless tools are: Terraform, AWS CloudFormation, Pulumi, and Ansible.