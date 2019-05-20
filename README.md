# Sample Java Web App in Spring Boot framework with Containerization (Plus Kubernetes NGINX Ingress Controller Deployment)
Readme update 1.1

## Highlevel Diagram To Illustrate What We Are Going To Create (Red Circle)
![Alt text](/diagram1.JPG "diagram1")

# In this sample, I'm using my Private Registry (Azure Container Registry - ACR) to deploy any PODs in K8S.

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

## Build 1st Java Spring Boot Micro-service (Apple)
```shell
/sb-web-apple/mvn package
```

## Build 2nd Java Spring Boot Micro-service (Banana)
```shell
/sb-web-banana/mvn package
```

## Create Secret Object In K8S To Store Private Registry (Azure Container Registry - ACR) Login
kubectl create secret docker-registry qooacr01 --docker-server=qooacr01.azurecr.io --docker-username=LOLLOL --docker-password=LOLLOLOLOLOLOLOL --docker-email=easonlai@msn.com

## Docker Build 1st & 2nd Java Spring Boot Micro-service And Push to Private Registry (Azure Container Registry - ACR)
```shell
docker build -t easonlai/sb-web-apple .
docker build -t easonlai/sb-web-banana .
docker tag easonlai/sb-web-apple qooacr01.azurecr.io/sb-web-apple
docker tag easonlai/sb-web-banana qooacr01.azurecr.io/sb-web-banana
docker push qooacr01.azurecr.io/sb-web-apple
docker push qooacr01.azurecr.io/sb-web-banana
```

## Pull Image and Push to Private Registry (Azure Container Registry - ACR)
```shell
docker tag quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.24.1 qooacr01.azurecr.io/nginx-ingress-controller:0.24.1
docker push qooacr01.azurecr.io/nginx-ingress-controller:0.24.1
```


