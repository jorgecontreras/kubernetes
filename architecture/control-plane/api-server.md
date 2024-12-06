# Kubernetes API Server

The **API Server** is the entry point to the Kubernetes control plane. It handles all REST requests and updates the cluster state accordingly.

---

## **Key Functions**
1. **Authentication**: Verifies user identities and permissions.
2. **API Endpoint**: Exposes a REST API for CRUD operations on Kubernetes objects.
3. **Cluster State Management**: Updates etcd with changes to cluster state.

---

## **Common Endpoints**

List all resources
  ```bash
  kubectl api-resources
  ```

Check version
  ```bash
  kubectl version
  ```

## References:

[Documentation](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/)