# Kubelet: The Node Agent

The **kubelet** is a key component of the Kubernetes worker node. It ensures that containers in a Pod are running as specified by the control plane.

---

## **Responsibilities**
1. **Pod Management**: Monitors and manages the lifecycle of all Pods on the node.
2. **Node Communication**: Communicates with the API server to get work instructions and send status updates.
3. **Health Checks**: Monitors the health of Pods using liveness and readiness probes.
4. **Logs and Metrics**: Collects logs and resource metrics for debugging and monitoring.
