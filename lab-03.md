# Lab 03 - Deployment Introduction

## Show Deployment

```
$ kubectl get deployment
```

__In short__

```
$ kubectl get deploy
```

## Create a Deployment with command

```
$ kubectl run nginx --image=nginx
```

Output

```
deployment.apps/nginx created
```

__Inspect__

```
$ kubectl get deployments
```

Output

```
NAME      DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
nginx     1         1         1            1           2m
```

```
$ kubectl get replicasets
```

Output

```
NAME               DESIRED   CURRENT   READY     AGE
nginx-64f497f8fd   1         1         1         2m
```

```
$ kubectl get pods
```

Output

```
NAME                     READY     STATUS    RESTARTS   AGE
nginx-64f497f8fd-5d9s7   1/1       Running   0          2m
```

## Generate YAML template with command

```
$ kubectl run nginx --dry-run --image=nginx -o yaml
```

Output

```
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      run: nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```

## Try to delete a pod

__Open three terminal to watch changes__

```
$ kubectl get deployments -w
```

```
$ kubectl get replicasets -w
```

```
$ kubectl get pods -w
```

Delte the pod

```
$ kubectl delete pod $(kubectl get po -o jsonpath='{.items[0].metadata.name}')
```

## Clear

```
$ kubectl delete deployment nginx
```
