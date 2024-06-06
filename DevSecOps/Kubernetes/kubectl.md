kubectl is a command line tool provided by Kubernetes that allows us to communicate with a Kubernetes cluster's control plane.
## kubectl apply
Once you have defined your deployment and service configurations in the YAML file, the next step would be to apply them so Kubernetes can take the desired configuration and turn it into a running process(s). The command for this would be:
```bash
kubectl apply -f example-deployment.yaml
```
## kubectl get
The `kubectl get` command allows you to check the status of the Kubernetes processes. It is a very versatile command and one of the most used commands. The `get` command can also be used to check the state of resources by using the `-n` or `--namespace` argument followed by the namespace name. For example:
```bash
kubectl get -n example-namespace
```
## kubectl describe
This command can be used to show the details of a resource (or a group of resources). These details can help in troubleshooting or analysis situations. For example, say one of the pods in your cluster has started erroring out, and you want to get more information about the pod to try to determine why it has crashed. For example:
```bash
kubectl describe pod example-node -n example-namespace
```
The results of this command would include details about certain "events", which can help shine a light on what the issue.

Additionally, the same command can also be used to view details about Kubernetes secrets using:
```bash
kubectl describe secret admin-credentials
```
The results of this would include details about the "Data" being stored.
## kubectl logs
The kubectl logs command allows you to view the application logs of the erroring pods. For example:
```bash
kubectl logs example-pod -n example-namespace
```
## kubectl exec
The kubectl exec command will allow you to get inside a container and run commands. If a pod has more than one container, you can specify a container using the `-c` or `--container` flag. The `-it` flag runs the command in interactive mode, everything after `--` will be run inside the container:
```bash
kubectl exec -it example-pod -n example-namespace -- sh
```
## kubectl port-forward
The kubectl port-forward command allows you to create a secure tunnel between your local machine and a running pod in your cluster. An example of when this might be useful is when testing an application. We take the port that is used to expose these pods and map it to one of our local ports. For example, matching the target port which is `8080` to a local port `8090` would make the application accessible on our local machine at `http://localhost:8090`.

The resources specified are `resource-type/resource-name`. This would be done using the kubectl port-forward command with the following syntax:
```bash
kubectl port-forward service/example-service 8090:8080
```
## kubectl auth
This command is used to inspect authorization. One of its significant commands is `kubectl auth can-i` which checks whether an action is allowed. This can be done by using the following command:
```bash
kubectl auth can-i VERB [TYPE | TYPE/NAME | NONRESOURCEURL]
```
- **VERB** is a logical Kubernetes API verb like 'get', 'list', 'watch', 'delete', etc.
- **NONRESOURCEURL** is a partial URL that starts with "/".
- **NAME** is the name of a particular Kubernetes resource. This command pairs nicely with impersonation.

Full command example as follows:
```bash
kubectl auth can-i get secret/admin-creds --as=system:serviceaccount:default:regular-user
```