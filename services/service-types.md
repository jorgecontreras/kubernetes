# Service Types

Kubernetes supports several types of Services based on the use case. Each type determines how traffic is routed to the target Pods.

---

## **Service Types**

1. **ClusterIP (Default)**:
   - Exposes the Service internally within the cluster.
   - Example use case: Backend services accessible by other applications within the cluster.

2. **NodePort**:
   - Exposes the Service on a static port of each Node’s IP.
   - Example use case: Simple external access during development.

3. **LoadBalancer**:
   - Exposes the Service externally via a cloud provider’s load balancer.
   - Example use case: Public-facing applications like a web server.

4. **ExternalName**:
   - Maps the Service to an external DNS name.
   - Example use case: Accessing an external database or API.

---

## **Templates**

### ClusterIP Service (Default)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: clusterip-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

### NodePort Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nodeport-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
      nodePort: 30007
```

### LoadBalancer Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: loadbalancer-service
spec:
  type: LoadBalancer
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```