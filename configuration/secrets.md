# Secrets in Kubernetes

A Secret is a Kubernetes object used to store sensitive data, such as passwords, tokens, and certificates. Secrets provide a secure way to manage sensitive information in the cluster.

## Key Features

- Base64 Encoding:
Secrets store data encoded in Base64 for transport but are not encrypted by default.
- Pod Integration:
Use Secrets as environment variables or mounted volumes.
- Types of Secrets:
Opaque (default): User-defined key-value pairs.
Built-in Types: E.g., kubernetes.io/tls, kubernetes.io/dockerconfigjson.

## Creating a Secret

from literal key-valuue pairs
```
kubectl create secret generic example-secret --from-literal=username=admin --from-literal=password=secret
```

from a file
```
kubectl create secret generic example-secret --from-file=credentials.txt
```

from a YAML manifest
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: example-secret
type: Opaque
data:
  username: YWRtaW4=  # Base64 for "admin"
  password: c2VjcmV0  # Base64 for "secret"
```
```
kubectl apply -f secret.yaml
```

## Using a Secret

as environment variables

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
        - name: SECRET_USERNAME
          valueFrom:
            secretKeyRef:
              name: example-secret
              key: username

```
as a mounted volume

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
        - name: secret-volume
          mountPath: /etc/secret
  volumes:
    - name: secret-volume
      secret:
        secretName: example-secret
```

