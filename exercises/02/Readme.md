## Create a pod

### How to run the sample

Find file named sidecar-pod.yaml in the same folder and run the pod:

```bash
kubectl apply -f sidecar.yaml
```

#### Once the pod is running, connect to the sidecar pod

```bash
kubectl exec sidecar-sample -c sidecar-container -it -- bash
```

#### Install curl on the sidecar

```bash
apt-get update && apt-get install curl
```

#### Use curl to access the log file via the sidecar

```bash
curl 'http://localhost:80'
```