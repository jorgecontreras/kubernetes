# etcd: The Distributed Key-Value Store

**etcd** is a critical component of the Kubernetes control plane. It serves as the backing store for all cluster data.

---

## **Features**
1. **High Availability**: Designed to run in a cluster to tolerate failures.
2. **Data Consistency**: Ensures strong consistency for cluster state and configuration.
3. **Key-Value Store**: Stores data as simple key-value pairs.

---

## **What is Stored in etcd?**
- Cluster state: Nodes, Pods, ConfigMaps, Secrets, etc.
- Resource configurations: Deployments, Services, and more.
- Metadata for events and scheduling.

# References:
[etcd](https://etcd.io/)