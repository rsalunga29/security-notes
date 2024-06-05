## Virtualization Levels
Hypervisor virtualisation (e.g. VMware) enables multiple virtual machines to run on a single physical server. Imagine a physical server in a data centre. Using a hypervisor, this server’s resources (CPU, storage, etc.) can be divided and dedicated to separate virtual machines within this server.

Containerization (platform example: Docker) is virtualization at an operating system level, meaning the same operating system kernel is used to run multiple containers.
## Use of Virtualization in IaC
1. **Scalability**: IaC uses virtualization to meet demands. If there is a sudden increase in demand and there is a need for more servers, virtual machines can be created to handle this increased load.
2. **Resource Isolation**: Using IaC, you can define what components get how much of the available resources. This means if one component starts consuming all of its allocated resources, it wont affect the performance of other components.
3. **Testing / Snapshots / Rollbacks**: The consistency that IaC provides allows OS virtualization and software configuration to be packaged and deployed anywhere. Also combined with the ability to take snapshots at specific points in time, rollbacks can be done if a deployment has gone wrong.
4. **Templates**: IaC uses templates to provision new instances, which ensures consistence across instances due to manual provision and