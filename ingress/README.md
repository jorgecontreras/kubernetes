# Ingress

**Ingress** is a Kubernetes object that provides HTTP and HTTPS routing to Services within a cluster. It acts as a centralized entry point for external traffic, enabling advanced routing and load balancing.

## **Why Use Ingress?**

**Centralized Access**:
Consolidates access to multiple Services through a single URL or load balancer.
   
**Advanced Routing**:
Supports hostname-based and path-based routing.
   
**TLS Termination**:
Handles HTTPS traffic by terminating SSL/TLS at the ingress point.

**Cost Efficiency**:
Replaces the need for multiple cloud provider load balancers when using LoadBalancer Services.

---

## **Ingress Controller**

Ingress requires an **Ingress Controller**, a pod that processes Ingress resources and routes traffic accordingly.

1. Common Ingress Controllers:
   - NGINX
   - Traefik
   - HAProxy
   - Cloud-provider-specific controllers (e.g., AWS ALB).

2. Install NGINX Ingress Controller:
   ```bash
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
   ```

## Template
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: basic-ingress
spec:
  rules:
    - host: example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-service
                port:
                  number: 80
```
>This routes traffic for http://example.com/ to the my-service on port 80.