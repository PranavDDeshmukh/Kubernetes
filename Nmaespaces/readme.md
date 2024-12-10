## Namespace 
**In Kubernetes, namespaces provide a mechanism for isolating groups of resources within a single cluster**

### List Namespaces
````
kubectl get namespace
````
````
kubectl get ns
````

### Create Namespacec
````
kubectl create ns dev
````

### Create pod in dev namespace
````
kubectl apply -f pod.yaml -n dev
````
````
kubectl get pod -n dev
````

### Namespace using yaml
````
apiVersion: v1
kind: Namespace
metadata:
  name: prod
````
````
kubectl apply -f ns.yaml
````
### Switch default to prod namespace
````
kubectl config set-context --current --namespace=prod
````
### View current namespace
````
kubectl config view --minify | grep namespace:
````
### Create pod in prod namespace
````
apiversion: v1
kind: Pod
metadata:
 namespace: prod
 name: pod-test
spec:
 containers:
 - name: c1
   image: nginx
   ports:
   - containerPort: 80
````
````
kubectl apply -f prod.yaml
````
