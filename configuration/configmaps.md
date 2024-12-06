# ConfigMaps in Kubernetes

A ConfigMap is a Kubernetes object used to store non-sensitive configuration data in key-value pairs. It allows separating configuration from application code, making applications more portable and easier to manage.

## Key Features

- Centralized Configuration:
Store environment variables, command-line arguments, or configuration files.
- Pod Integration:
Inject configuration into Pods as environment variables or mounted volumes.
- Decoupling:
Keep configurations outside the application container images for flexibility.

## Creating a Configmap

From literal key value pairs:
```
kubectl create configmap example-config --from-literal=key1=value1 --from-literal=key2=value2
```

from a file:
```
kubectl create configmap example-config --from-file=config-file.properties
```

from a yaml manifest:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: example-config
data:
  key1: value1
  key2: value2
```

```
kubectl apply -f configmap.yaml
```

## Using a Configmap

as environment variables:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
    - name: example-container
      image: nginx
      env:
        - name: ENV_VAR
          valueFrom:
            configMapKeyRef:
              name: example-config
              key: key1
```

as mounted volume:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
    - name: example-container
      image: nginx
      volumeMounts:
        - name: config-volume
          mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: example-config

```

