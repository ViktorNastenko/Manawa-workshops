# Connect my Frontend application to Database

```
$ oc set env dc/manawa-todo -e MONGODB_USER=mongodbuser -e MONGODB_PASSWORD=mongodbpass -e MONGODB_DATABASE=todolist -e DATABASE_SERVICE_NAME=mongodb.devweek-<LDAP>-todolist.svc
```

