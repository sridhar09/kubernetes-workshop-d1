## Replication

So what if we want to scale-out our application for resilience and high
availability? Sounds like we need to create more of them pods... Here's where
the ReplicaSet comes in handy.

```
kubectl apply -f replicaset.yaml
```

This will create our replicaset configured to replicate 3 pods. Let's check it
out:

```
kubectl get rs
kubectl get pod
```

As you can see we have three pods running right now. But wait, why are they
three when we instructed the RestfulSet to bring up three and we had one
already created statically from before? It's simple, the first pod we created
has the same label as the pods managed by the ReplicaSet, this means that the
ReplicaSet will count that in as well as long as its selector will match it.

The ReplicaSet will always maintain a fixed number of pods as per its
configuration. Think of it as a means to group multiple pods of the same type
together. If one pod is terminated, a new pod will be crated in its place.

Let's delete our initially created static pod and see what happens.

```
$ kubectl delete -f ../01/simple-pod.yaml
```

_NOTE: We used the manifest file to delete the pod resource, however supplying
the pod name would work as well, you don't need the manifest to delete
resources._

Let's check the pods now and see what's going on:

```
$ kubectl get pod
```

Looks like there are still 3 pods & all of them are controlled by the replicaset

### Scaling a Replicaset

We can upscale or downscale our replicaset

```
kubectl scale --replicas=2 rs/getting-started
```

This downscales the replicaSet to 2 pods from 3

```
kubectl get pods
```

As you can see we only have 2 pods running now

```
kubectl scale --replicas=4 rs/getting-started
kubectl get pods
```

This upscale the replicaSet from 2 pods to 4 pods

We can also set autoscaling rule.

```
kubectl autoscale rs getting-started --min=2 --max=5 --cpu-percent=80
```

We can also set much more detailed upscaling & downscaling rule using scaling policy yaml. Follow [this documentation](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) for further details

###Clean up

```
kubectl delete rs/getting-started
```