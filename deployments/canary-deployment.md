# Canary Deployment

A canary deployment is a progressive release strategy where a small percentage of traffic is routed to a new version of an application to test its stability. If the canary behaves as expected, the new version is gradually rolled out to all users.

This document outlines two simple, Kubernetes-native approaches to achieve a canary deployment.

## Method 1: Traffic Splitting with Label Selectors

Use Kubernetes label selectors and Services to route traffic proportionally based on Pod replica counts. This approach leverages native Kubernetes resources without the need for custom controllers or third-party tools.

#### 1. Deploy the Stable and Canary Versions

Use Deployments with labels to differentiate between stable and canary Pods.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: brew
spec:
  replicas: 5
  selector:
    matchLabels:
      app: brew
  template:
    metadata:
      labels:
        app: brew
        version: stable
    spec:
      containers:
      - name: brew
        image: brew:stable
        ports:
        - containerPort: 80
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: brew-canary
spec:
  replicas: 1
  selector:
    matchLabels:
      app: brew
  template:
    metadata:
      labels:
        app: brew
        version: canary
    spec:
      containers:
      - name: brew
        image: brew:canary
        ports:
        - containerPort: 80


```

#### Define a Single Service Targeting Both Versions

Create a Service that selects Pods from both Deployments. Kubernetes will route traffic proportionally based on the number of replicas.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: brew-service
spec:
  selector:
    app: brew
  ports:
  - port: 80
    targetPort: 80

```

## Method 2: Weighted Traffic Splitting with Ingress

Use an Ingress Controller (e.g., NGINX) to route traffic between the stable version and the canary version based on percentages. The traffic split is managed by the Ingress annotations and is independent of the number of replicas.

#### Deploy the Stable and Canary Versions

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: brew-stable
spec:
  replicas: 10
  selector:
    matchLabels:
      app: brew
      version: stable
  template:
    metadata:
      labels:
        app: brew
        version: stable
    spec:
      containers:
      - name: brew
        image: brew:stable
        ports:
        - containerPort: 80
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: brew-canary
spec:
  replicas: 1  
  selector:
    matchLabels:
      app: brew
      version: canary
  template:
    metadata:
      labels:
        app: brew
        version: canary
    spec:
      containers:
      - name: brew
        image: brew:canary
        ports:
        - containerPort: 80

```
#### Define separate services

```yaml
apiVersion: v1
kind: Service
metadata:
  name: stable-service
spec:
  selector:
    app: brew
    version: stable
  ports:
  - port: 80
    targetPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: canary-service
spec:
  selector:
    app: brew
    version: canary
  ports:
  - port: 80
    targetPort: 80
```

#### Create an Ingress with Weighted Traffic Routing: 

The Ingress annotations control the traffic split, not the number of Pods.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: brewapp-stable-ingress
spec:
  rules:
  - host: brew.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: stable-service
            port:
              number: 80
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: brewapp-canary-ingress
  annotations:
    nginx.ingress.kubernetes.io/canary: "true"        # Marks this as a canary rule
    nginx.ingress.kubernetes.io/canary-weight: "20"  # Sends 20% of traffic to canary
spec:
  rules:
  - host: brew.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: canary-service
            port:
              number: 80

```

#### Result:

- 80% of traffic goes to brew:stable.
- 20% of traffic goes to brew:canary.
- The split remains consistent regardless of the number of replicas (10 stable vs. 1 canary).

## TL;DR

- Use Method 1 (labels) for simplicity, non-HTTP workloads, or lightweight canary deployments.
- Use Method 2 (Ingress) for precision, HTTP workloads, and production-grade control.
