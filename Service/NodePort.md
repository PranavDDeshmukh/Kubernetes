## Node Port Range 30000 - 32767
## NodePort
````
apiVersion: v1
kind: Pod
metadata:
 name: frontend
 labels:
   app: frontend-app
spec:
  containers:
  - name: c1
    image: abhipraydh96/docker-app
    ports:
    - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: net-service
spec:
  selector:
    app: frontend-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort
````
### Commands:
````
kubectl apply -f node-deploy.yaml
````
````
kubectl get deploy
kubectl get svc
kubectl get pod
````
````
kubectl get node -o wide
````
![image](https://github.com/user-attachments/assets/7e0fc1a0-4b6c-4ce5-ba23-ed36b5dddad0)
