## Namespaces
Namespaces in Kubernetes are used to isolate groups of resources within a single cluster. Resources must be uniquely named within a namespace, but the same resource name can be used across different namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc.) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc.).
## ReplicaSet
A ReplicaSet maintains a set of replica pods and can guarantee the availability of x number of identical pods.
> Identical pods are helpful when a workload needs to be distributed between multiple pods.

ReplicaSets usually aren't defined directly, but are instead managed by a deployment.
## Deployments
Deployments are used to define a desired state. One the desired state is defined, the deployment controller process changes the actual state to the desired state.

Deployments also provide declarative updates for pods and replica sets. In other words, if a user defined a deployment named `test-nginx-deployment`, and wrote a definition that the deployment must have a ReplicaSet containing three nginx pods. Once this deployment is defined, the ReplicaSet will create pods in the background.
## StatefulSets
To understand StatefulSets, one must first understand the difference between stateful and stateless apps.


### Stateful vs Stateless Apps
Stateful apps store and record user data, allowing them to return to a particular state. Stateless applications, however, have no knowledge of any previous user interactions as it does not store user session data.