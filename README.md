# Reddit Clone App on Kubernetes with Ingress
This project demonstrates how to deploy a Reddit clone app on Kubernetes with Ingress and expose it to the world using Minikube as the cluster.
Below is an overview of the architecture of this Reddit Clone App running on Kubernetes with Ingress.
![Architecture Diagram](https://github.com/LondheShubham153/reddit-clone-k8s-ingress/assets/71492927/e1eec5f2-1983-445b-8966-e9acfdea7f8e)

## Prerequisites
Before you begin, you should have the following tools installed on your local machine: 

- Docker
- Minikube cluster ( Running )
- kubectl
- Git

You can install Prerequisites by doing these steps. [click here & complete all steps one by one]().


# Step 1: Install Docker and Minikube
sudo apt-get update
sudo apt install docker.io

# Step 2: Install minikube using link or install using below cmd:https://minikube.sigs.k8s.io/docs/start/
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

The "docker" driver should not be used with root privileges. If you wish to continue as root, use --force.
If you are running minikube within a VM, consider using --driver=none:
minikube status

minikube start --force ... if as root user

# Step 3: Install Kubectl

sudo snap install kubectl --classic

kubectl get po -A

# Step 4 clone the project and build image

git clone https://github.com/RushikeshVikhe/Ingress_minikube_reddit_clone_k8s.git

Go inside path cd Ingress_minikube_reddit_clone_k8s

docker build -t reddit-clone-app .

docker images

# Step 5: Enable below ports 3000,31000,443,80 

# Step 6: Push image on docker hub and create deployment, service

Push image on dockerHub

cd /Ingress_minikube_reddit_clone_k8s/k8s

kubectl apply -f deployment.yaml

kubectl get deployment

kubectl apply -f service.yaml

minikube service reddit-clone-service --url

curl -L http://192.168.49.2:31000

# Step 7: Port Forwording and Ingress 
To view in browser using -Then We have to expose our app service-

First We need to expose our deployment so use-

kubectl expose deployment reddit-clone-deployment --type=NodePort

kubectl port-forward svc/reddit-clone-service 3000:3000 --address 0.0.0.0

search in browser - your instace_public_ip:3000(takes litle time to load- 15to20 secs)

kubectl apply -f ingress.yaml

if you got error while applying ingress- use below cmd and then apply ingress again

kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission

kubectl get ingress

curl -L domain.com/test
