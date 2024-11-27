### Replicaset using euqlity based selector:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: rs-1
spec:
  replicas: 3
  selector:
    matchLabels:
     app: nginx-app
  template:
    metadata:
      name: tmp-nginx
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx-cont
        image: nginx
```

### Replicaset using set based selector:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: rs-demo

spec:
  replicas: 3
  selector:
    matchExpressions:
    - key: app
      operator: In
      values: 
      - nginx-app

  template:
    metadata:
      name: tmp-nginx
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx-cont 
        image: nginx
```

````
kubectl apply rs.yaml
````
````
kubectl get rs
````
````
kubectl get pods
````
````
kubectl delete rs rs-demo
````

