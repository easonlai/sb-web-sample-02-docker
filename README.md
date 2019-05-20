# Sample Java Web App in Spring Boot framework with Containerization (Plus Kubernetes NGINX Ingress Controller Deployment)
Readme update 1.0

## Highlevel Diagram To Illustrate What We Are Going To Create (Red Circle)
![Alt text](/diagram1.JPG "diagram1")

## Create New Dev Namesapce in K8S
```shell
kubectl apply -f namespace-dev.json
```

## Create NGINX Ingress Controller Pods and Necessary Components in K8S
```shell
kubectl apply -f mandatory.yaml
```

## Deploy 1st Load Balance Sample App (Apple) in K8S
```shell
kubectl apply -f apple.yaml
```

## Deploy 2nd Load Balance Sample App (Banana) in K8S
```shell
kubectl apply -f banana.yaml
```

## Create NGINX Ingress Controller Service in K8S
```shell
kubectl apply -f ingress-nginx.yaml
```

## Configure NGINX Ingress Controller Rules in K8S
```shell
kubectl apply -f ingress.yaml
```

## Check NGINX Ingress Controller Service IP (Internal IP) in K8S
```shell
kubectl get services ingress-nginx-apple-banana
```

## Test Service
```shell
http://INTERNAL_IP/apple
http://INTERNAL_IP/banana
```
