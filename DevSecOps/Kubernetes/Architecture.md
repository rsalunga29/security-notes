## Cluster Architecture
### Pods
Pods are the smallest deployable unit of computing we can create and manage in Kubernetes. Pods are essentially a group of one or more containers, that share storage and network resources. Because of this, containers on the same pod can communicate easily as if they were on the same machine whilst maintaining a degree of isolation.

Pods are treated as a unit of replication, meaning if a workload (application) needs to be scaled up, we will increase the number of pods running.
### Nodes
Nodes are essentially where pods runs on. There are two types of nodes. The control plane (master node) and worker nodes. Nodes can either be a physical or virtual machine.

Easier way of understanding what nodes are: if applications run in containers which are placed in a pod, nodes contain all the services necessary to run pods.
### Clusters
At the highest level, we have our Kubernetes Cluster; put simply, a Cluster is just a set of nodes. Every cluster has at least one worker node.
## Kubernetes Control Plane
The control plane (master node) manages the worker nodes and pods in the cluster. It does this with the use of various components:
### Kube-apiserver
The API server is the front-end of the control plane and is responsible for exposing the Kubernetes API. The kube-apiserver component is scalable, meaning multiple instances can be created so traffic can be load-balanced.
### Etcd
Etcd is a key/value store containing cluster data / the current state of the cluster. It is highly available and consistent. Any changes made in the cluster is reflected in etcd. The other control plane components rely on etcd as an information store and query it for information such as available resources.
### Kube-scheduler
The kube-scheduler component actively monitors the cluster. Its job is to assign newly created pods into nodes. It makes this decision based on specific criteria, such as the resources used by the running application or available resources on all worker nodes.
### Kube-controller-manager
This component is responsible for running the controller processes, such as the node controller process which is responsible for noticing when nodes go down. The controller manager would then talk to kube-scheduler to schedule a new node to come up.

There are many different types of controllers. Some examples of them are:
- **Node controller**: Responsible for noticing and responding when nodes go down.
- **Job controller**: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
- **EndpointSlice controller**: Populates EndpointSlice objects (to provide a link between Services and Pods).
- **ServiceAccount controller**: Create default ServiceAccounts for new namespaces.
The above is not an exhaustive list.
### Cloud-controller-manager
This component enables communication between a Kubernetes cluster and a cloud provider API. It's main purpose is to allow the separation of components that communicate internally within the cluster and those that communicate externally by interacting with the cloud provider. This also allows cloud providers to release features at their own pace.

![[control-plane.png]]
## Kubernetes Worker Node
Worker nodes are responsible for running and maintaining pods, reports to the control plane (master node), and doing any work assigned to them by the control plane (master node). The following components are present on every worker node:
### Kubelet
Kubelet is an agent that runs on every node in the cluster and is responsible for ensuring that containers are running in a pod. It does this by taking a set of PodSpecs and ensures that the containers described in those PodSpecs are running and healthy. It executes actions given to it by the controller-manager.
### Kube-proxy
Kube-proxy is responsible for network communication within the cluster. It makes networking rules so traffic can flow and be directed to a pod (from inside or outside of the cluster). A traffic won't directly reach a pod, instead it will reach a Service (which would be associated with a group of pods) first, and then gets redirected to one of the associated pods.
### Container runtime
Pods have containers running inside of them. A container runtime must be installed on each node for this to happen. One of the most popular choice is Docker.

![[worker-node.png]]
## Communication Between Components
![[component-comms.png]]