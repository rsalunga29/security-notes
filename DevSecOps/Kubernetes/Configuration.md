## Config File
Kubernetes config files are typically written in YAML format (best practice). But, they can also be made interchangeably using the JSON format.

The following are the four fields which must be present in each of the YAML files:
### apiVersion
The version of the Kubernetes API you are going to use to create this object. The API version you use will depend on the object being defined. A cheatsheet for what API version to use for which object can be found [here](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-apiversion-definition-guide.html).
### kind
What kind of object you are going to create (e.g. Deployment, Service, StatefulSet).
### metadata
This will contain data that can be used to uniquely identify the object (including name and an optional namespace).
### spec
The desired state of the object (for deployment, this might be 3 nginx pods).
### example-service.yaml
```yaml
apiVersion: v1
kind: Service
metadata:
	name: example-nginx-service
spec:
	selector:
		app: nginx # since nginx is defined, this service will look for apps with the nginx label
	ports:
		- protocol: TCP
		  port: 8080 # the port the service is exposed on
		  targetPort: 80 # the port to which the service will send requests
	type: ClusterIP
```
### example-deployment.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
	name: example-nginx-deployment
spec:
	replicas: 3 # tells k8s we want 3 replicas in this ReplicaSet
	selector:
		matchLabels:
			app: nginx
	template: # the template k8s use to create pods
		metadata: # template identifier
			labels:
				app: nginx
		spec: # template specs, k8s uses this to know which image and settings to use
			containers:
				- name: nginx
				  image: nginx:latest
				  ports:
					  - containerPort: 80 # must match with the targetPort in the service file.
```