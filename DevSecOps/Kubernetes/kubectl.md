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
This command can be used to show the details of a resource (or a group of resources). These details can help in troubleshooting or analysis situations. For example, say one of the pods in your cluster has started erroring out, and you want to get more information about the pod to try to determine why it has crashed. You would run the following command:
```bash
kubectl describe pod example-nod -n example-namespace
```
The results of this command would include details about certain "events", which can help shine a light on what the issue.
## kubectl logs
