# kubeconfig: Kubernetes Configuration File

The **kubeconfig** file is a YAML file that provides configuration details for connecting to a Kubernetes cluster.

---

## **Purpose**
1. Stores cluster connection information (e.g., API server URL, authentication tokens).
2. Allows users to interact with multiple clusters seamlessly.

---

## **File Format**
Example `~/.kube/config`:

```yaml
apiVersion: v1
clusters:
- cluster:
    server: https://<cluster-endpoint>
    certificate-authority: /path/to/ca.crt
  name: my-cluster
contexts:
- context:
    cluster: my-cluster
    user: admin
  name: my-context
current-context: my-context
users:
- name: admin
  user:
    client-certificate: /path/to/client.crt
    client-key: /path/to/client.key
```

## Useful Commands

View current context:
```bash
kubectl config current-context
```

Switch context:
```bash
kubectl config use-context <context-name>
```

List all contexts:
```bash
kubectl config get-contexts
```