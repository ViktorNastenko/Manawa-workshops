
## Autoscale my application

Set CPU and Memory limits on your deployment:

```
    $ oc set resources dc manawa-todo --limits=cpu=200m,memory=512Mi --requests=cpu=100m,memory=256Mi 
```

Then, configure the auto-scaling:

```
    $ oc autoscale dc manawa-todo --min 1 --max 10 --cpu-percent=80
```

Check :

```
    $ oc get hpa
```

Finally, launch an ab testing:

```
    $ ab -n 10000 -c 20 https://manawa-todo-workshop-<LDAP>-todolist.euw1-gcp-poc.adeo.cloud/tasks
```

And now check hpa and pods:

```
    $ oc get hpa && oc get po && oc get dc
```
