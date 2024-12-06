# Kubernetes Scheduler

The **Kubernetes Scheduler** is a core control plane component responsible for assigning Pods to nodes based on resource availability and scheduling policies.

---

## **Responsibilities**
1. **Pod Placement**:
   - Determines the best node to run a Pod based on resource requests, constraints, and policies.
   - Pods in the `Pending` state are processed by the scheduler.

2. **Resource Optimization**:
   - Balances workloads across nodes to ensure efficient resource utilization.

3. **Policy Adherence**:
   - Applies scheduling rules such as affinity, anti-affinity, and tolerations.

---

## **How the Scheduler Works**
1. The API server receives a new Pod definition.
2. The Pod enters the `Pending` state and is added to the scheduler's queue.
3. The scheduler evaluates all nodes in the cluster based on:
   - **Node Filters (Predicates)**: Excludes nodes that don't meet basic requirements (e.g., insufficient resources, taints).
   - **Node Scoring (Priorities)**: Assigns a score to eligible nodes based on factors like available resources and affinity.
4. The highest-scoring node is selected, and the scheduler binds the Pod to that node.

