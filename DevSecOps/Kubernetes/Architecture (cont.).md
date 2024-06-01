## Namespaces
Namespaces in Kubernetes are used to isolate groups of resources within a single cluster. Resources must be uniquely named within a namespace, but the same resource name can be used across different namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc.) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc.).
## ReplicaSet
A ReplicaSet maintains a set of replica pods and can guarantee the availability of x number of identical pods.
> Identical pods are helpful when a workload needs to be distributed between multiple pods.

ReplicaSets usually aren't defined directly, but are instead managed by a deployment.
## Deployments
Deployments are used to define a desired state.