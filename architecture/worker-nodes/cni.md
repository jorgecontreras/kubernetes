# CNI (Container Network Interface): Networking Plugin

CNI is a network interface standard that Kubernetes uses to manage Pod networking.

## Role:

- Provides network connectivity to Pods.
- Assigns IP addresses to Pods and ensures communication between them.
- Handles additional features like network policies and traffic isolation.

## Placement:

CNI plugins are installed on worker nodes and integrate with Kubernetes networking components like kube-proxy.

## How It Works:

- When a Pod is created, Kubernetes calls the CNI plugin to configure the Pod’s network namespace.
- The CNI plugin connects the Pod to the cluster network and assigns an IP address.

## Popular CNI Plugins:

- Calico: Advanced networking and network policies.
- Flannel: Simple overlay network.
- Weave Net: Peer-to-peer mesh networking.
- Cilium: Network policies with eBPF support.
