# Expose my application to everyone with Public IP

get the service to expose:

```
$ oc get svc
NAME          CLUSTER-IP      EXTERNAL-IP   PORT(S)     AGE
manawa-todo-service   172.30.62.149   <none>        8080/TCP    25s
mongodb       172.30.178.29   <none>        27017/TCP   4h
```

create the route
```
$ oc create route edge --service manawa-todo-service --port 8080
or
$ oc create –f route.yaml
```


Finaly, check:
```
$ oc get routes
```

> * Now test your application on https://manawa-todo-devweek-<YOUR LDAP ID>-todolist.euw1-gcp-poc.adeo.cloud
> * Normaly connection to database failed...
