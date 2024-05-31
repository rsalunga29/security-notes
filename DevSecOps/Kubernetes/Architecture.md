## Cluster Architecture
### Pods
Pods are the smallest deployable unit of computing we can create and manage in Kubernetes. Pods are essentially a group of one or more containers, that share storage and network resources. Because of this, containers on the same pod can communicate easily as if they were on the same machine whilst maintaining a degree of isolation.

Pods are treated as a unit of replication, meaning if a workload (application) needs to be scaled up, we will increase the number of pods running.
### Nodes
Nodes are essentially where pods runs on. There are two types of nodes. The control plane (master node) and worker nodes. Nodes can either be a physical or virtual machine.

Easier way of understanding what nodes are: if applications run in containers which are placed in a pod, nodes contain all the services necessary to run pods.
### Clusters
At the highest level, we have our Kubernetes Cluster; put simply, a Cluster is just a set of nodes.
## Kubernetes Control Plane
The control plane (master node) manages the worker nodes and pods in the cluster.