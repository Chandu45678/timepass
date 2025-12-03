✅ STEP 1 — Start Minikube

Run:

minikube start


Check if it is running:

kubectl get nodes


You must see:

minikube   Ready

✅ STEP 2 — Create MySQL Deployment YAML

Create file:

mysql-deployment.yaml


Paste:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: rootpass
        ports:
        - containerPort: 3306

✅ STEP 3 — Apply Deployment
kubectl apply -f mysql-deployment.yaml


Check pods:

kubectl get pods

✅ STEP 4 — Scale the MySQL Deployment

Scale from 1 → 3 pods:

kubectl scale deployment mysql --replicas=3


Check status:

kubectl get deployments
kubectl get pods -l app=mysql


You will now see 3 MySQL pods.

✅ STEP 5 — Scale Down (optional)

Scale from 3 → 1:

kubectl scale deployment mysql --replicas=1


Check pods:

kubectl get pods