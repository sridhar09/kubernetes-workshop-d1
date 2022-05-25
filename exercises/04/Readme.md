## Deployments

How do we do a rolling update of our application right now? Well, it's not
easy. You would need to create a new replicaset for the new version and then
scale in the old replicaset and clean it up yourself, which is a bit annoying.
That's why Kubernetes introduced the Deployment resource.

```
$ kubectl apply -f deployment.yaml
```

_NOTE: If you look at its manifest, the deployment looks identical to the
ReplicaSet, aside from the `kind` atttribute that is. The reason is that
Deployments are controllers for replicasets, they basically work by creating,
scaling and removing replicasets._

Our deployment should be now created:
```
kubectl get deployments -o wide
```

_NOTE: The `-o wide` argument instructs kubectl to format the output in wide
mode which will show some extra information dependening on the resource kind
being listed._

```
kubectl get pods 
kubectl get rs 
```

Pods & ReplicaSets were automatically created due to deployment creation


### Rolling update

Now let's make a change to our deployment so that an update takes place:

```
kubectl set image deployment/getting-started getting-started=docker/getting-started:vscode
```

Now, if we look at the pods :
```
kubectl get pods
```
we'll see that the rolling update process started
and new pods are being launched. They are being replaced one by one by the
deployment logic.


Let's check out the replicasets:

```
kubectl get rs
```

You should see two replicasets, one is the old one which has desired size set
to 0 and the other is the new one which has desired size set to 3.

### Useful deployment related commands

We can check the rollout status of a deployment by running:

```
kubectl rollout status deployment getting-started
```

To see the deployment rollout history you can run:

```
kubectl rollout history deployment getting-started
```

This will give us a list of revisions with their respective change cause.

### Rollback

To rollback to the previous deployment revision you can simply run:

```
$ kubectl rollout undo deployment getting-started
```

If you need to rollback to a specific revision then use the `--to-revision`
argument:

```
$ kubectl rollout undo deployment getting-started --to-revision=2
```
