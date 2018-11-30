# Manage my application (log, rsh, debug)

Check logs:

```
$ oc get po

$ oc logs po/XXX
```


Go inside your pod:

```
$ oc rsh po/XXX
```


Test these commands:

```
$ oc describe <something>

$ oc export <something>

$ oc whoami –c|-t

$ oc get pv

$ oc get pvc

...
```


