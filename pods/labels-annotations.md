# Labels and Annotations

**Labels** and **Annotations** are metadata added to Kubernetes objects like `Pods`, `Services`, and `Deployments`. They help organize, select, and manage resources.

---

## Labels

**Purpose**:
   - Used to identify and group resources.
   - Commonly used for selectors in Services and Deployments.

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: example-pod
    labels:
    app: my-app
    environment: production
```

**Selector**
```yaml
selector:
  app: my-app
```

view labels
```bash
kubectl get pods --show-labels
```

## Annotations

**Purpose**

Used to add non-identifying metadata (e.g., build info, URLs, owners).
Not used for selectors.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
  annotations:
    description: "This is an example pod"
    owner: "team@example.com"
```

view annotations

```bash
kubectl describe pod example-pod | grep Annotations
```


