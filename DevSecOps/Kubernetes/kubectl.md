kubectl is a command line tool provided by Kubernetes that allows us to communicate with a Kubernetes cluster's control plane.
## kubectl apply
Once you have defined your deployment and service configurations in the YAML file, the next step would be to apply them so Kubernetes can take the desired configuration and turn it into a running process(s). The command for this would be:
```bash
kubectl apply -f example-deployment.yaml
```
## kubectl get
