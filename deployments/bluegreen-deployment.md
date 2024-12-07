# Blue/Green Deployment 

A blue/green deployment is a deployment strategy where two identical environments (blue and green) are maintained. One environment serves production traffic, while the other is updated with a new version of the application. Once validated, traffic is switched to the new version.

This strategy minimizes downtime and allows easy rollback if issues occur.

## How Blue/Green Works in Kubernetes

In Kubernetes, a blue/green deployment involves creating two versions of an application:

- Blue (current): The version currently serving production traffic.
- Green (new): The version being deployed and tested.

Traffic switching can be handled in several ways:

- By updating a Service's selector to point to the green version.
- By using Ingress or a load balancer to direct traffic to the green version.

## Method 1: Service Selector Switching (Kubernetes-Native)

In this method, the Kubernetes Service acts as the traffic switch. You deploy both versions (blue and green) but only one version is selected by the Service at a time.

deploy blue

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: brew-blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: brew
      version: blue
  template:
    metadata:
      labels:
        app: brew
        version: blue
    spec:
      containers:
      - name: brew
        image: brew:1.0
        ports:
        - containerPort: 80
```

deploy green

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: brew-green
spec:
  replicas: 3
  selector:
    matchLabels:
      app: brew
      version: green
  template:
    metadata:
      labels:
        app: brew
        version: green
    spec:
      containers:
      - name: brew
        image: brew:2.0
        ports:
        - containerPort: 80

```

Create a Service to Switch Traffic: Initially, the Service points to the blue version.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: brew-service
spec:
  selector:
    app: brew
    version: blue
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

switch traffic

```bash
kubectl patch service brew-service -p '{"spec":{"selector":{"app":"brew","version":"green"}}}'
```

if something goes wrong, rollback
```bash
kubectl patch service brew-service -p '{"spec":{"selector":{"app":"brew","version":"blue"}}}'
```

## Method 2: Ingress-Based Traffic Switching

This method uses an Ingress Controller (e.g., NGINX) to control traffic between Brew-Blue and Brew-Green.

create separate services for blue and green

```yaml
apiVersion: v1
kind: Service
metadata:
  name: blue-service
spec:
  selector:
    app: brew
    version: blue
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: green-service
spec:
  selector:
    app: brew
    version: green
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

create Ingress for blue-service

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: brewapp-ingress
spec:
  rules:
  - host: brew.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: blue-service
            port:
              number: 80
```

create Ingress for green-service

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: brewapp-ingress
spec:
  rules:
  - host: brew.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: green-service
            port:
              number: 80
```

deploy by applying green-ingress

```bash
kubectl apply -f ingress-green.yaml
```

rollback by applying blue-ingress

```bash
kubectl apply -f ingress-blue.yaml
```

