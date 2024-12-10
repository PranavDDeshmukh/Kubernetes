
````
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dep-1
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
````

## Rolling Updates and Rollback
**Update deployment version**
````
kubectl set image deployment/dep-1  nginx-cont=nginx:1.14.1  --record
````
**Check revision history**
````
kubectl rollout history deployment/dep-1
````
**Rollback to previous version**
````
kubectl rollout undo deployment/dep-1
````
**Rollback to perticular revision**
````
kubectl rollout undo deployment/dep-1 --to-revision=2
````

