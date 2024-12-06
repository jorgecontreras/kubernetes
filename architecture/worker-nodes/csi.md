# CSI (Container Storage Interface): Storage Plugin

CSI is a storage interface that allows Kubernetes to use external storage providers in a standardized way.

## Role:

- Provides a consistent API for Kubernetes to manage storage (e.g., volumes, snapshots).
- Enables the use of cloud-based storage systems (AWS EBS, GCP Persistent Disks) and on-premises storage solutions.

## Placement:

CSI drivers run as custom controllers or DaemonSets within the cluster, interfacing with the Kubernetes control plane and worker nodes.

## How It Works:

- Kubernetes interacts with storage providers through the CSI driver to dynamically provision Persistent Volumes (PVs).
- The CSI driver abstracts the underlying storage technology, making it seamless to use.

## Example:

When a PersistentVolumeClaim (PVC) is created, Kubernetes uses the CSI driver to allocate storage from a storage provider.