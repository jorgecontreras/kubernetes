# kubernetes

## Components

**Pod** 

Collections of containers collocated in a single machine

**Service** 

Load balancer that can bring traffic to a collection of pods

**Deployment** 

Replicate a container for availability or scale.

**Kubelet** 

The primary node agent that runs on each node.

![](media/architecture.jpeg)

![](media/pod.jpeg)

![](media/deployments.jpeg)

![](media/services.jpeg)

## Basic Commands

create deployment:

`kubectl create -f helloworld-pod-with-labels.yml`
  
get pods:

`kubectl get pods`
  
get pods with labels:

`kubectl get pods --show-labels`
  
rename label:

`kubectl label pod/helloworld app=helloworldapp --overwrite`
  
delete label:

`kubectl label pod/helloworld app-`
  
selectors:

```
  kubectl get pods --selector env=production --show-labels
  kubectl get pods --selector dev-lead=jorge,env=staging --show-labels
  kubectl get pods --selector dev-lead!=jorge,env=staging --show-labels
  kubectl get pods -l 'release-version in (1.0,2.0)' --show-labels
```

delete pods with label:

`kubectl delete pods -l dev-lead=jorge`


replace service:

`kubectl replace --force -f commerce.yaml`

deployments:

```
kubectl set image deployments/commerce commerce-app=jorgecontreras/commerce:0.8 --v 6
kubectl rollout history deployments commerce
kubectl describe deployments commerce
kubectl rollout undo deployment commerce --to-revision=2

```

scale:

`kubectl scale --replicas=10 deployment commerce`

(GKE) resize cluster size:

`gcloud container clusters resize monarca --num-nodes=3`

### Imperative approach

```
$ kubectl create namespace ckad
$ kubectl run nginx --image=nginx --restart=Never -n ckad
$ kubectl edit pod/nginx -n ckad
```

### Declarative approach

Suitable for more elaborate changes, version controlled.

```
$ vim niginx-pod.yaml
$ kubectl create -f nginx-pod.yaml
$ kubectl delete pod/nginx
```
### Hybrid approach

```
$ kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > nginx-pod.yaml
$ vim niginx-pod.yaml
$ kubectl apply -f nginx-pod.yaml
```

# CKAD 

## Core Concepts

### Creating a pod and inspecting it

1. Create the namespace `ckad-prep`
2. 2. In the namespace `ckad-prep` create a new Pod named `mypod` with the image `nginx:2.3.5`. Expose port 80
3. Identify the issue with creating the container. Write down the root cause of issue in a file named `pod-error.txt`
4. Change the image of the Pod to `nginx:1.15.12`
5. List the Pod and ensure that the container is running
6. Log into the container and run the `ls` command. Write down the output. Logout of the container.
7. Retrieve the IP address of the Pod `mypod`
8. Run a temporary Pod using the image `busybox`, shell into it adn run a `wget` command against the `nginx` Pod using port 80
9. Render the logs of Pod `mypod`
10. Delete the Pod and the namespace
