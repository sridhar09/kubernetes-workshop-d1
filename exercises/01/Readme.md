## Create a pod

In this exercise, we are going to use the `docker/getting-started` image. But feel free to use any image from docker hub, or your custom image instead.

Now let's create our pod:

```
kubectl apply -f pod.yaml
```

And now let's see if it's running:

```
kubectl get pods
```

if your pod is in the ContainerCreating or Pending state, wait for the pod to be in running state before moving ahead.

_NOTE: The `metadata.name` field in the manifest is the name that our resource
will have assigned, this name should always be unique in the scope of the
namespace._


### We have a pod, what next? How can we interact with it?

You can actually exec into the pod (if there's a shell or bash etc. available in the image
of course). We are going to `sh` in this case.
```
kubectl exec -ti getting-started -- sh
```
This should bring up the shell prompt and voila, you're in!

You can use curl command to hit localhost:80.

```
curl localhost:80
```

You will see the raw HTML of the getting started webpage.

Run `exit` command to exit the container.

### What else can I do with this pod?

Luckly we can actually port forward a localhost port the pod, here's how:

```
kubectl port-forward pod/getting-started 8080:80
```

This basically binds localhost:8080 to our pod's 80 port. You can now access
http://localhost:8080

_NOTE:_
1. _Only TCP is currently supported for port forwarding and it can work for
Pod, ReplicaSet, Deployment and Service resources._
2. _All ports <1024 are privileged port and require special permissions. This is the reason we will not be able to run `kubectl port-forward pod/getting-started 80:80`_