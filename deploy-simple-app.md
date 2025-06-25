# 🚀 Deploying a Simple API to AWS EKS (EC2 Node + NodePort)

This guide walks you through creating an EKS cluster and deploying a Dockerized API with NodePort access — no Fargate, no ALB, just EC2.

---

## ✅ Prerequisites

Make sure you have the following installed:

- AWS CLI  
- `eksctl`  
- `kubectl`  
- Docker  

---

## 🔐 Step 1: Configure AWS CLI

```bash
aws configure
Enter:

Access Key

Secret Key

Region (e.g., us-east-1)

Output format (e.g., json)

☸️ Step 2: Create EKS Cluster (with EC2 Nodes)
bash
Copy
Edit
eksctl create cluster \
  --name demo-cluster \
  --region us-east-1 \
  --nodegroup-name linux-nodes \
  --node-type t3.medium \
  --nodes 2 \
  --managed
⏳ This takes ~15 minutes. It sets up:

VPC

Control plane

EC2 worker nodes

🔁 Step 3: Connect kubectl to Cluster
```sh
    aws eks update-kubeconfig --name demo-cluster --region us-east-1
```
kubectl get nodes
🐳 Step 4: Build and Push Docker Image
If using DockerHub:
```sh
docker build -t yourusername/myapi:latest .
docker push yourusername/myapi:latest
```
🚀 Step 5: Deploy API on EKS
clone the repository
```sh
   https://github.com/WhiteboxHub/classroom-cicd-kubernetes.git
   cd classroom-cicd-kubernetes
```
## Deploy manifesto 
```sh
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f configMap.yaml
```
🌐 Step 6: Access Your API
Get the public IP of any EC2 worker node:
```sh
kubectl get nodes -o wide
```
Access the API using:
```sh
http://<EC2-PUBLIC-IP>:30080
```
🧹 Cleanup
To delete everything:
```sh
eksctl delete cluster --name demo-cluster --region us-east-1
```
🙌 That's it!
You now have a working EKS cluster running a Dockerized API with NodePort access. 🚀


## Contributors
whitebox-learning!