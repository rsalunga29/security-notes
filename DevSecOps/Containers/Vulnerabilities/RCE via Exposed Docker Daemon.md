Docker can also use TCP sockers to facilitate communication between the host OS and containers.

Docker can be remotely administrated. For example, using management tools such as Portainer or Jenkins to deploy containers to test their code.
## The Vulnerability
The Docker Engine will listen on a port when configured to be run remotely. The Docker Engine is easy to make remotely accessible but difficult to do securely. The vulnerability here is Docker is remotely accessible and allows anyone to execute commands.
## Check if Target Has Docker Remotely Accessible
By default, Docker engine will run on port `2375`. We can confirm this by running a port scan against the target.

Once confirmed, we are going to use the `curl` command to interact with the exposed Docker daemon: `curl http://docker-ip-address:2375/version`.
## Executing Docker Command on Target
We can now execute Docker commands on our target. For example, start containers, stop containers, delete them, or export the contents of the containers for us to analyse further. 

by using the following command: `docker -H tcp://docker-ip-address:2375 COMMAND`.

The `COMMAND` parameter refers to Docker commands, such as `network ls`, `images`, `exec`, or `run`.