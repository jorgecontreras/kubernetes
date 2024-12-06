# Deployment Basics

A **Deployment** in Kubernetes is a higher-level object that manages Pod replicas, provides rolling updates, and ensures the desired state of an application is maintained.

---

## **Key Features**
1. **Replica Management**:
   - Ensures a specified number of Pod replicas are running at all times.
2. **Rolling Updates**:
   - Gradually updates Pods to the latest version with minimal downtime.
3. **Self-Healing**:
   - Automatically replaces failed or terminated Pods.

---

## **Creating a Deployment**

```
kubectl create deployment backend -n ckad --image=nginx --replicas=3
```

### YAML Example:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: api
  template:
    metadata:
      labels:
        app: api
    spec:
      containers:
        - name: nginx
          image: nginx:1.21.6
          ports:
            - containerPort: 80
```

list deployments
```
kubectl get deployments
```

inspect a deployment
```
kubectl describe deployment backend
```

check the deployment's pods
```
kubectl get pods -l app=api
```