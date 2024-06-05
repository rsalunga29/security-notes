## Agent-based
Agent-based IaC needs an "agent" to be installed on the server that is to be managed. It runs in the background and acts as a communication channel between the IaC tool and the resources that need managing. This agent is responsible or executing and reporting on the state of the infrastructure/managed resource.

An agent-based IaC tool can perform tasks even when the system has limited connectivity or is offline, making it a robust choice for automation. It is important to continuously monitor the agent software closely so that it can be restarted in the event of a crash.

Some agent-based IaC tools will also require opening ports on the server for inbound and outbound traffic, allowing the agent to push/pull configuration information.

Examples of agent-based IaC tools are: Puppet, Chef, and Saltstalk.