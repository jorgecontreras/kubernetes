# Kubernetes Architecture Overview

Kubernetes is a container orchestration platform designed to automate deployment, scaling, and management of containerized applications. Its architecture consists of **control plane components** and **worker nodes**.

---

## **Key Components**

### 1. **Control Plane**
- **API Server**: Front-end for the Kubernetes cluster. It processes REST API calls and updates the cluster state.
- **etcd**: A distributed key-value store for storing cluster configuration and state.
- **Controller Manager**: Ensures that the desired state of the cluster matches the actual state.
- **Scheduler**: Assigns Pods to nodes based on resource availability and scheduling policies.

### 2. **Worker Nodes**
- **Kubelet**: Node agent that ensures Pods are running on the node.
- **Kube-proxy**: Manages network rules to enable communication between Pods and Services.
- **Container Runtime**: Responsible for running containers (e.g., Docker, containerd).

---

## **Control Plane Diagram**
![](../media/architecture.jpeg)

---

Explore individual components in detail:
- [kubelet](worker-nodes/kubelet.md)
- [etcd](control-plane/etcd.md)
- [api-server](control-plane/api-server.md)
- [kubeconfig](kubeconfig.md)
