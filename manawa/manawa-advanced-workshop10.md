# Change my application release (rolling update)


Change imageStream manually :

```
$ oc tag quay.io/adeo/manawa-todo:v2 manawa-todo:latest
```

Also, you replace the existing image tag by a new one (remote).


Check :

```
$ oc rollout status  dc/manawa-todo
$ oc get dc
```

* Finally, check your new application release !

https://manawa-todo-devweek-<LDAP>-todolist.euw1-gcp-poc.adeo.cloud


