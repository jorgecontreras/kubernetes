# Rolling Updates

Rolling updates ensure that application changes (such as new container images) are deployed incrementally with minimal downtime.

---

## Performing a Rolling Update

update deployment image

```bash
kubectl set image deployment/backend nginx=nginx:1.23.0
```

monitor the update
```
kubectl rollout status deployment/backend
```

verify the new pods
```
kubectl get pods -l app=api
```