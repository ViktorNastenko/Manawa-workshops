# Change my application release (rolling update)


Change imageStream manually :

```
$ oc tag quay.io/adeo/manawa-todo:v2 manawa-todo:latest
```

Also, you replace the existing image tag by a new one (remote).

```
$ oc rollout status  dc/manawa-todo
```

* Finally, check your new application release !

https://manawa-todo-workshop-<LDAP>-todolist.euw1-gcp-poc.adeo.cloud

The new release must hurt your eyes !

Note : if you get a timeout it is not an error. 