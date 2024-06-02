Docker can also use TCP sockers to facilitate communication between the host OS and containers.

Docker can be remotely administrated. For example, using management tools such as Portainer or Jenkins to deploy containers to test their code.
## The Vulnerability
The Docker Engine will listen on a port when configured to be run remotely. The Docker Engine is easy to make remotely accessible but difficult to do securely. The vulnerability here is Docker is remotely accessible and allows anyone to execute commands.
## Check if Target Has Docker Remotely Accessible
By default, Docker engine will run on port `2375`.