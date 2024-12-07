A **Service** in Kubernetes is an abstraction that provides a stable endpoint for accessing a set of Pods. Services ensure that communication between applications or with external clients remains consistent, even if Pod IPs change.

![](../media/services.jpeg)

## Why Use Services?

- **Dynamic Pod IPs** Pods have ephemeral IP addresses. Services provide a consistent DNS name or IP.

- **Load Balancing**
Services can distribute traffic across multiple Pods.
   
- **Access Control**:
Control which Pods or clients can access specific Pods.

---

## **Creating a Service**

### Example: Exposing a Deployment with a ClusterIP Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

```bash
kubectl apply -f service.yaml
```

expose deployment

```bash
kubectl expose deployment my-app --type=ClusterIP --port=80 --target-port=8080
```

view services across namespaces

```bash
kubectl get services -A
```