# Expose my application to internal cluster with Private IP

Expose the service to internal cluster

```
$ oc create -f service.yml
```

```
service "manawa-todo-service" created
```
This command create a service, an endpoint inside the Openshift cluster.