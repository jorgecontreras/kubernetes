# Scaling Deployments

Scaling a deployment adjusts the number of Pod replicas to match application needs. This ensures high availability and efficient resource usage.

## manual scaling
scale with kubectl:
```bash
kubectl scale deployment example-deployment --replicas=5
```

scale by editing the deployment YAML file
```yaml
spec:
  replicas: 5
```
```
kubectl apply -f deployment.yaml
```

verify scaling updates
```
kubectl get deployment backend
kubectl get pods -l app=api
```


## autoscaling

Enable horizontal pod autoscaling (HPA) to dynamically adjust replicas based on CPU or memory usage.

create HPA:
```
kubectl autoscale deployment example-deployment --cpu-percent=50 --min=2 --max=10
```

view HPA:
```
kubectl get hpa
```