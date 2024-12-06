# Multi-Container Pods

**Multi-container Pods** allow multiple containers to run together in a single `Pod`. They share the same network namespace and can communicate via `localhost`.

---

## Use Cases

**Sidecar Containers**:
   - Enhance the primary container by handling auxiliary tasks like logging or caching.
   - Example: A container to ship logs to an external system.

**Ambassador Containers**:
   - Act as a proxy between the main container and an external system.

**Init Containers**:
   - Run before the main containers to perform setup tasks like downloading files.

---

## Sidecar Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-container-pod
spec:
  containers:
    - name: app-container
      image: nginx
    - name: log-shipper
      image: busybox
      command: ["sh", "-c", "tail -f /var/log/nginx/access.log"]
```

## Init Container Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-container-example
spec:
  initContainers:
    - name: init-container
      image: busybox
      command: ["sh", "-c", "echo Initializing"]
  containers:
    - name: app-container
      image: nginx
```