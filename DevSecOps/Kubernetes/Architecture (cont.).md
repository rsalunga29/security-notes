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

Essentially, StatefulSets allows stateful applications to run on Kubernetes, but unlike pods in a deployment, they cannot be created in any order and will have a unique ID associated with each pod. This unique ID is persistent, meaning if a pod fails, it will be brought back up and keep this ID.

StatefulSets will have one pod, referred to as the master pod, which can read/write to the database. The other pods, referred to as slave pods, can only read and have their own replication of the storage. All pods are continuously synchronized to ensure changes from the master pod is reflected to the slave pods.
![[statefulsets.png]]
### Stateful vs Stateless Apps
Stateful apps store and record user data, allowing them to return to a particular state. Stateless applications, however, have no knowledge of any previous user interactions as it does not store user session data.
## Services
A service is basically an abstraction that is used to expose a group of pods over a network. Since pods are ephemeral, meaning they are spun-up and destroyed regularly, they can't be issued an IP address, because doing so would change the IP address every time a pod is destroyed and spun-up. Instead, services are used so that a single static IP can be associated with a pod and its replicas.

There are different types of services you can define: `ClusterIP`, `LoadBalancer`, `NodePort` and `ExternalName`.
![[services.png]]