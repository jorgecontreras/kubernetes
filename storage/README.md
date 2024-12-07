# Volumes

A **Volume** in Kubernetes is a directory accessible to containers within a `Pod`. It abstracts storage from the container’s lifecycle, ensuring data persistence even if the container restarts.

## Why Use Volumes?

**Data Persistence**: Retain data across container restarts.

**Shared Storage**: Share data between multiple containers in a Pod.

**Flexibility**: Integrate with cloud storage, network file systems, or local storage.

## Types of Volumes

**EmptyDir**:
A temporary storage volume tied to the Pod's lifecycle.

```yaml
volumes:
- name: temp-storage
    emptyDir: {}
```

**HostPath**:
Mounts a directory from the host node.

```yaml
volumes:
- name: host-storage
    hostPath:
    path: /data
```

**PersistentVolume (PV)**:
Represents a piece of storage in the cluster provisioned by an admin. Used with [PersistentVolumeClaims](pv-and-pvc.md) (PVCs).

**ConfigMap/Secret Volumes**:
Mounts ConfigMaps or Secrets as files.

---

## Templates

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-with-volume
spec:
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
        - name: temp-storage
          mountPath: /usr/share/nginx/html
  volumes:
    - name: temp-storage
      emptyDir: {}