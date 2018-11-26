# Manage my application (log, rsh, debug)

1. Check logs:
```
$ oc get po
$ oc logs po/XXX
```


2. Go inside your pod:
```
$ oc rsh po/XXX
```


3. Test those commands:
```
$ oc describe <something>
$ oc export <something>
$ oc whoami –c|-t
$ oc get pv
$ oc get pvc
...
```


