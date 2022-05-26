## Create a pod

### How to run the sample

Find file named sidecar-pod.yaml in the same folder and run the pod:

```bash
kubectl apply -f persistent-volume.yaml
kubectl apply -f persistent-volume-claim.yaml
kubectl apply -f deployment.yaml
```

```
kubectl exec <pod-in-deployment> -- touch /pv01/sample.txt
```

```
kubectl exec <another-pod-in-deployment> -- ls
```

The files are persisted across pods.