**Log into Manawa using oc**

In your terminal, login using your LDAP account: 

```
$ oc login -u <LDAP> -p <LDAP_PASSWORD> https://manawa.euw1-gcp-poc.adeo.cloud/
```

**Choose a namespace (project) that will contain your application**

```
$ export PROJECT_NAME=[YOUR NAMESPACE NAME]
```

```
$ oc project $PROJECT_NAME
```

**Use/create a service account**

Your team might already have a service account.

Use the following command to list the existing service account and find the one matching your team.

```
$ oc get sa
```

Service account follow this format svc-[BU]-[Project] (e.g svc-adeo-software-factory or svc-adeo-manawa)

If you don't find any service account matching your team, then you can create a new one using the following command

> /!\ only do this if you haven't found a service account matching your team when using the command: "oc get sa":

```    
$ export MANAWA_USER=[YOUR SERVICE ACCOUNT]
```

```
$ oc create sa $MANAWA_USER
```

**Generate a manawa token for your service account**

```
$ oc sa get-token $MANAWA_USER # Copy it somewhere we will need it later
```

**Create a secret containing the JFrog credentials**

```
$ oc create secret docker-registry registry-artifactory --docker-server=<your_jfrog_repository> --docker-username=<your_service_account_username> --docker-password=<your_service_account_password> --docker-email=<your_service_account_email>
```

> Note:
As example for your_jfrog_repository variable in the previous command: adeo-docker-adeo-manawa-dev.jfrog.io

**Give the default service account the ability to connect to JFrog**

```
$ oc secrets link serviceaccount/$MANAWA_USER secrets/registry-artifactory --for=pull
```

**Install helm tiller inside your namespace**

```
$ export TILLER_NAMESPACE=$PROJECT_NAME
```

```
$ oc policy add-role-to-user edit system:serviceaccount:$TILLER_NAMESPACE:$MANAWA_USER
```

```
$ helm init --service-account=$MANAWA_USER
```
