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

