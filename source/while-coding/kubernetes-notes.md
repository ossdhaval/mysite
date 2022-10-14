# Kubernetes Notes

## then and now

earlier :

we used to have applications deployed on clusters of web-servers ( like websphere, tomcat etc ) and there was a load-balancer which was managing load across all those. In this, what was missing is when one of the server nodes in the cluster goes down. You needed to manually intervene and bring up a new node. All the network configurations were manual too. The load balancer only managed load with available server nodes in the cluster. It could not scale by creating new servers as needed and destroying those which were not needed. 

With kubernetes :

It manages the containers ( start, stop, check health etc )
It eliminates single point of failure ( like load balancer ealier )
Scale containers by create more containers if needed
Update the containers without bringing down the application
it also manages networking and interconnections among containers
plus, facilities like service discovery, configuration management etc

## Key things in kubernetes setup :



## why should a developer learn kubernetes :

Emulate production environment locally to :
ensure that application scales properly
ensure that secrets and configs are working properly
Performance testing along with scaling
How to install and run kubernetes on local machine :

there are few options :

Docker desktop : most preferred and easiest. But has limitation where you can have only one master and one node. Can't scale out. But it is not available for Linux. 
minikube : best bet for Linux development machines and created by Kubernetes project itself. 
Kind
kubeadm : this is fully fledged kubernetes

For production ready light-weight kubernetes, look at k3s(by Rancher), microk8s(by Ubuntu/canonical). 
Here, light-weight means they have lesser memory footprint. See this for comparison. 

https://www.itprotoday.com/cloud-computing-and-edge-computing/lightweight-kubernetes-showdown-minikube-vs-k3s-vs-microk8s#:~:text=Minikube%20is%20the%20easiest%20overall,configure%20than%20the%20other%20distributions.

We will go with minikube here.

## install minikube :
reference : https://minikube.sigs.k8s.io/docs/start/

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb

sudo dpkg -i minikube_latest_amd64.deb

minikube start
```

Now install kubectl :

```
sudo snap install kubectl --classic
```

Starting kubernetes dashboard :

```
minikube dashboard
```

## Kubernetes PODs :

- Pod is the smallest and most basic unit for Kubernetes
- Pod provides environment for container to run
- Pod can have multiple containers, but mostly generally, it is used to host one container
- Pod has its own IP address, memory, volumes.
- Pod, once destroyed, can never be resurrected.
- One node can have multiple pods. One pod can have multiple containers. Each pod has unique IP address. So if the app is running on different pods, it can listen on the same Port. But if an app is running on containers on the same POD then each instance need to use a different port.

### Creating a pod :

Create a pod

```
kubectl run my-first-pod --image=nginx:alpine
```

check if the pod has been created 

```
kubectl get all
```

Accessing service on that Pod :

```
kubectl port-forward my-first-pod 8080:80
```

Keep the process running

now go to browser and hit 'localhost:8080'. You should see welcome page of nginx

here in command, 8080 is external port, request to which is being forwarded to internal port 80 of cluster IP of pod where the container is listening

deleting the pod

```
kubectl delete pod my-first-pod
```

### Creating POD using YAML :


Simple yaml :

use create, apply commands when creating pod using yaml. If you are not using yaml then you can directly use 'kubectl run' as mentioned above.

```
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx
  labels:
    app: nginx
    rel: stable
spec:
  containers:
  -    name: my-nginx
       image: nginx:alpine
       ports:
       - containerPort: 80
```

To create pod:
```
kubectl create -f ~/code/docker-kubernetes/dk/src/nginx.pod.yaml --save-config
```

To get list:
kubectl get all

To get more details about pod :
kubectl describe pod my-nginx

To get access to shell of the container running inside the pod :
kubectl exec my-nginx -it sh
(you can find your html files hosted with nginx under '/usr/share/nginx/html/' )

To delete the pod :
kubectl delete -f ~/code/docker-kubernetes/dk/src/nginx.pod.yaml

Configuring liveness and readiness probs : 

