# PersistentVolumes (PV) and PersistentVolumeClaims (PVC)

**PersistentVolumes (PV)** and **PersistentVolumeClaims (PVC)** are Kubernetes objects that manage durable storage for Pods. They decouple storage provisioning from Pod configuration.

## PersistentVolume (PV)

Represents a physical storage resource in the cluster. Provisioned by an admin or dynamically via a StorageClass.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
    name: example-pv
spec:
    capacity:
    storage: 10Gi
    accessModes:
    - ReadWriteOnce
    hostPath:
    path: /data/pv
```

## PersistentVolumeClaim (PVC)

It represents a request for storage. Binds a PV that meets the specified requirements.

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: example-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

## Binding

The PVC binds to a PV that matches the requested accessModes and storage.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-with-pvc
spec:
  containers:
    - name: app-container
      image: nginx
      volumeMounts:
        - name: persistent-storage
          mountPath: /usr/share/nginx/html
  volumes:
    - name: persistent-storage
      persistentVolumeClaim:
        claimName: example-pvc
```

## StorageClass

Automates PV provisioning when a PVC is created.

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
```

PVC using above storage class
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: standard


```