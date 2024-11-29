## ConfigMaps
- Store non-sensitive configuration data, such as key-value pairs of strings or Base64-encoded binary data.
- ConfigMaps are used to keep configuration values separate from code and container images. 

````
apiVersion: v1
kind: ConfigMap
metadata:
  name: db-credentials
data:
  DB_URL: "mydbinstance.c6c8dfghilnt.us-east-1.rds.amazonaws.com"
  DB_USERNAME: "admin"
````


## Secrets
- Store sensitive information, such as passwords, tokens, or keys, as base64-encoded data.
- Secrets are used to keep confidential data separate from app code.

**To encrypt password**
````
echo -n 'passws123' | base64
````
**To decrypt password**
````
echo -n 'bXlzZWNyZXRwYXNzd29yZA== ' | base64 --decode
````


````
apiVersion: v1
kind: Secret
metadata:
  name: db-password
type: Opaque
data:
  password: UGFzc3dkMTIzJA==  # Base64 encoded value of 'password'
````

**deployment file**
````
apiVersion: apps/v1
kind: Deployment
metadata:
  name: docker-app
  labels:
    app: docker-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: docker-app
  template:
    metadata:
      labels:
        app: docker-app
    spec:
      containers:
      - name: docker-app
        image: abhipraydh96/docker-app
        ports:
        - containerPort: 80
        env:
        - name: DB_URL
          value: "database-1.cnee62wsiw85.ap-southeast-1.rds.amazonaws.com"
    
        - name: DB_USERNAME
          value: "mydatabase"
        - name: DB_USERNAME
          valueFrom:
            secretKeyRef:
              name: db-credentials
              key: DB_USERNAME
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-password
              key: password
        resources:
          requests:
            memory: "128Mi" # Minimum memory guaranteed
            cpu: "250m"     # Minimum CPU guaranteed
          limits:
            memory: "256Mi" # Maximum memory allowed
            cpu: "500m"     # Maximum CPU allowed
````

