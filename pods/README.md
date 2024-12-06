A **Pod** is the smallest deployable unit in Kubernetes. It represents a single instance of a running process in your cluster and can contain one or more tightly coupled containers.

![](../media/pod.jpeg)

## **Key Features of Pods**

1. **Single or Multi-Container Workloads**:
   - Typically runs one container, but can include additional helper containers.

2. **Shared Resources**:
   - Containers within a Pod share:
     - Network namespace: They communicate via `localhost`.
     - Storage volumes.

3. **Ephemeral by Nature**:
   - Pods are designed to be temporary. Use higher-level controllers like Deployments to manage them.

## Creating a pod

```bash
kubectl run nginx --image=nginx:1.17.10 -n ckad --port=80
```

get pods
```bash
kubectl get pod -n ckad
```

create temporary pod
```bash
kubectl run temporary -it --rm --restart=Never --image=busybox -n ckad -- wget 10.244.1.2:80
```

create a pod YAML template
```bash
kubectl run hello --image=busybox -n ckad --dry-run=client -o yaml > pod.yaml -- /bin/sh -c "echo 'Hello World'"
```

create pod from YAML file
```bash
kubectl apply -f pod.yaml
```

get pod logs
```bash
kubectl logs hello -n ckad
```

inspect pod
```bash
kubectl describe hello -n ckad
```

delete a pod
```bash
kubectl delete pod hello -n ckad
```
