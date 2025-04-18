# Single Kubernetes MYSQL pod with Load Balancer, Persistent Volume and Persistent Volume Claim running on Minikube

This repository contains YAML configurations to deploy a **Single Kubernetes MYSQL pod with Load Balancer, Persistent Volume and Persistent Volume Claim running on Minikube**.

## 🛠️ Features
- **Load Balancer**
- **Persistent Volume**
- **Persistent Volume Claim** 

## 📌 Prerequisites
- Minikube (`v1.35.0`)

## 🚀 Deployment Steps
1. Clone this repo:
   ```sh
   git clone https://github.com/rinavillaruz/kubernetes-mysql-single-pod-pvc.git
2. Install Minikube.
3. Use portforward instead of NodePort for Mac
```sh
kubectl port-forward svc/mysql-service 3306:3306
```
4. Create a directory for mysql-data and mysql-dump.
5. Install tmux.
5. Use tmux to mount it and run on the background
```sh
tmux new-session -d -s mysql-data-mount 'minikube mount $HOME/minikube-volumes/mysql-data:/data'
tmux new-session -d -s mysql-dump-mount 'minikube mount ~/minikube-volumes/mysql-dump:/dump'
```

## 📝 To connect to MySQL using any client, when you do port-forwarding, you will see something like this:
```sh
    Forwarding from 127.0.0.1:3306 -> 3306
    Forwarding from [::1]:3306 -> 3306
    Handling connection for 3306
    Handling connection for 3306
```
Use 127.0.0.1 as host, 3306 as port, root as username and password

## 📝 To import a dump sql file
   ```sh
      kubectl get pods
      kubectl exec -it <pod-name> -- /bin/bash
      mysql -u root -p database_name < dump.sql
   ```