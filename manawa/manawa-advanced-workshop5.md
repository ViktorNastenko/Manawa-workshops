# Deploy frontend application

deploy your application :

```
$ oc create -f todo.yaml
```

```
imagestream "manawa-todo" created
```

```
deploymentconfig "manawa-todo" create
```


It will update your deployment by setting environment variables which contain the credentials of your mongo database.

Of course it is a demo example, for production you can use vault and consul.