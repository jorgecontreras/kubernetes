# Rollbacks

Rollbacks revert a Deployment to a previous state, ensuring application stability when an update fails.

## Rollback to a Previous Revision

list rollout history

```bash
kubectl rollout history deployment/backend
```

rollback to the Last Known Good State:

```bash
kubectl rollout undo deployment/backend
```

rollback to a Specific Revision:

```
kubectl rollout undo deployment/backend --to-revision=2
```