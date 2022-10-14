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

- Docker desktop : most preferred and easiest. But has limitation where you can have only one master and one node. Can't scale out. But it is not available for Linux. 
- minikube : best bet for Linux development machines and created by Kubernetes project itself. 
- Kind
- kubeadm : this is fully fledged kubernetes

For production ready light-weight kubernetes, look at k3s(by Rancher), microk8s(by Ubuntu/canonical). 
Here, light-weight means they have lesser memory footprint. See [this](https://www.itprotoday.com/cloud-computing-and-edge-computing/lightweight-kubernetes-showdown-minikube-vs-k3s-vs-microk8s#:~:text=Minikube%20is%20the%20easiest%20overall,configure%20than%20the%20other%20distributions.) for comparison. 



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

```
kubectl get all
```

To get more details about pod :

```
kubectl describe pod my-nginx
```

To get access to shell of the container running inside the pod :

```
kubectl exec my-nginx -it sh
(you can find your html files hosted with nginx under '/usr/share/nginx/html/' )
```

To delete the pod :

```
kubectl delete -f ~/code/docker-kubernetes/dk/src/nginx.pod.yaml
```

Configuring liveness and readiness probs : 

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
       livenessProbe:
         httpGet:
           path: /index.html
           port: 80
         initialDelaySeconds: 15
         timeoutSeconds: 2 #default: 1
         periodSeconds: 5 #default: 10
         failureThreshold: 1 #default: 3
       readinessProbe:
         httpGet:
           path: /index.html
           port: 80
         initialDelaySeconds: 3
         periodSeconds: 5 #default: 10
         failureThreshold: 1 #default: 3
```

## ReplicaSets and Deployment :

### ReplicaSet :
In Kubernetes, replicaset came into existance first and then deployments came in as wrapper of replicasets to further ease the configuration. 

self-healing is provided by replicasets. 
replicaset ensures that we have intended number of pods running at any time.
takes care of scaling when required

You don't need to create pods directly if you use replicaset.

### Deployment :

deployment is a wrapper around replicaset. Plus, deployment also adds support for zero-downtime deployments, roll-back of deployments ( pod template labels are useful here).

yaml of replicaset and deployment are almost same.

```
apiVersion: apps/v1 # this is mandatory attribute
kind: Deployment
metadata:
  name: my-frontend
  labels:
    app: frontend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: frontend
  template: # template can be stored in a separate file also
    metadata:
      labels:
        app: frontend
    spec:
      containers:
        - name: my-ngnix
          image: nginx:alpine
          ports:
            - containerPort: 80
          resources:
            limits:
              memory: "128Mi" #128 MB
              cpu: "200m" #200 millicpu (.2 cpu or 20% of the cpu)
```

Here, deployment will look for templates that has matching labels as mentioned in the selector section 

to start the deployment :

```
kubectl create -f ~/code/docker-kubernetes/dk/src/frontend.deployment.yaml --save-config
```

To get info about deployment :

```
kubectl describe deployment my-frontend
```

To see all the deployments along with their labels :

```
kubectl get deployment --show-labels
```

To see deployment with a certain label :

```
kubectl get deployment -l app=frontend
```

To scale a running deployment :
```
kubectl scale -f ~/code/docker-kubernetes/dk/src/frontend.deployment.yaml --replicas=4
```

or if you want to do via yaml then put the 'replica' entry in yaml as given above and then run apply as below:
```
kubectl apply -f ~/code/docker-kubernetes/dk/src/frontend.deployment.yaml
```

From here on, I have not listed everything in detail. Just commands and what they do. Need to go back and take more detailed notes from video below and onwards :

https://app.pluralsight.com/course-player?clipId=32f4f873-30d1-4a70-9cf0-510a899d2223


## zero downtime deployments :

here there are 4 versions of the same app which we are trying to deploy one after other :

yaml for all four are standard deployment yaml.

deployments are done with standard create or apply commands and deployment will take care of rolling deployments(zero down time ) automatically.

## creating services :

services are all about networking.

##### networking notes from (https://kubernetes.io/docs/concepts/services-networking/)

- Every Pod gets its own IP address. 
- Pods can be treated much like VMs or physical hosts from the perspectives of port allocation, naming, service discovery, load balancing, application configuration, and migration.
- containers within a Pod share their network namespaces - including their IP address and MAC address. This means that containers within a Pod can all reach each other's ports on localhost. This also means that containers within a Pod must coordinate port usage, but this is no different from processes in a VM. This is called the "IP-per-pod" model.


Kubernetes networking addresses four concerns:

- Containers within a Pod use networking to communicate via loopback.
- Cluster networking provides communication between different Pods.
- The Service resource lets you expose an application running in Pods to be reachable from outside your cluster.
- You can also use Services to publish services only for consumption inside your cluster.


## Helm

Reference: https://www.youtube.com/watch?v=Zzwq9FmZdsU&t=2s
