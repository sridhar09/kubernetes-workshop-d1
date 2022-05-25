## Create a service

Now that we have a pod, let's create a service object that would act as a proxy
for our pod.

```
$ kubectl apply -f service.yaml
```

And we should see our newly created service:

```
$ kubectl get svc

```

_NOTE: Our service is of type NodePort, this service type will create a unique
host port mapping which can be accessed from outside the cluster if needed.
Other types are ClusterIP (no host port mapping, only reachable from inside the
cluster network) and LoadBalancer (provisions a cloud provider load balancer
for our service)._

### Generating a URL

```
minikube service web-app --url
```

This command give a URL which can be used to access the exposed service