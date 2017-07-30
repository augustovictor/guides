# Kubernetes

## Definitions:
- Deployment: Responsible for keep `pods` running.
	- If a pod is deleted or crash the deployment will spin up another instance of it;
- Pods: Services like in a `docker-compose` file

## Commands

### Kubectl
**All commands start with** `kubectl`

Command | Description
---|---
`run webserver --image=nginx:alpine` | Start a `nginx` service named `webserver`
`get deployments` | List all deployments
`delete [pod, service] <instance_name>` | Delete a pod, service
`expose deployment webserver --type=LoadBalancer --port=80` | Expose the whole `webserver` deployment which will work as a load balancer in port `80`
`get services` | List running services (Here we can see the exposed deployment)
`create configmap node-app-config --from-file=path/to/file.yml` | Creates a configmap to be used by a service
`get configmap node-app-config -o yaml` | Prints the `node-app-config` to the console as `yaml`
`create -f deployments/node-app-config.yml` | Creates a deployment from a config file
`create -f services/node-app.yml` | Creates a service from a config file

### Observations
- When list the services the column `EXTERNAL-IP` will be set as `<pending>` because we're working locally. However it would have an actual IP address if we were in cloud; To get an IP we need to use `minikube` to create a VM;

**node-app-config** configmap

```YAML
from_literal=mongo_user=node-app-user
from_literal=mongo_password=passwd123
from_literal=mongo_host=$(minikube ip) # Returns the minikube VM ip address
```

***


### Minikube
**All commands start with** `minikube`

Command | Description
---|---
`start` | Start `minikube`
`docker-env` | Get docker client inside `minikube` VM
`service webserver --url` | Show the IP of a `minikube` VM with the running `webserver` service
`dashboard` | Dashboard with all deployments, services, pods, etc
`docker-env` | List the env variables of the minikube VM;
`eval $(minikube docker-env)` | Connect to the VM;

Set local docker client to point to the docker server inside `minikube` VM;

## Observations
- Use `minikube` to work with `kubernetes` locally. Istall `kubectl` first;
- To create a config file we first need to set the local docker to point to the docker server that runs inside the minikube VM;
- In order to use kubernetes to run containers with an application we first need to have a built image of it. `docker build -t <image_name>:1 .`;