# Super Mario Game Deployment on AWS EKS

**Reference Document** : https://mrcloudbook.com/deploying-super-mario-on-kubernetes/

# Project Overview

This project demonstrates a fun and interactive deployment of a Super Mario Game on an AWS Elastic Kubernetes Service (EKS) cluster. The entire AWS infrastructure is provisioned and managed using Terraform, showcasing Infrastructure as Code (IaC) practices for automating resource creation.

# Live Demo
Experience the app live: https://github.com/MBkalpana/K8S-Super-Mario
![image](https://github.com/user-attachments/assets/66dd37c3-4a31-41e7-96d1-8eff75edba2e)


# Prerequisites
Ensure the following tools are installed on your system:

**Terraform**/
**kubectl**/
**AWS CLI**

# The project is designed to:

+ Deploy the Super Mario game as a Kubernetes application.
+ Utilize Terraform to create a scalable, production-ready AWS environment.
+ Offer a simple and easy-to-replicate deployment process.

# Features:
+ **Infrastructure as Code:** Automated setup using Terraform for AWS resources.
+ **Kubernetes Deployment:** Application deployed on an AWS EKS cluster.
+ **Scalable Architecture:** Designed to support traffic spikes.
+ **Modern Practices:** Use of managed Kubernetes (EKS) for deployment.


# AWS Resources Created

Using Terraform, the following AWS resources are provisioned:

+ **VPC**: A Virtual Private Cloud with subnets, route tables, and an internet gateway.
+ **EKS Cluster**: A managed Kubernetes service for hosting the Super Mario game.
+ **Node Group**: EC2 instances managed by EKS for running Kubernetes workloads.
+ **IAM Roles**: IAM roles and policies for EKS and worker nodes.
+ **Security Groups:** Secure networking for the cluster and the game.

# Deployment Steps:

# Step1 : Create an EC2 Instance: 
![image](https://github.com/user-attachments/assets/9315c2b5-2375-4b69-9afc-3a8d2a4eceb3)

# Step2: Create IAM role and attach it to EC2 instance:
![image](https://github.com/user-attachments/assets/cc5b671b-000e-42a7-b61b-40ea5a468756)

![image](https://github.com/user-attachments/assets/20319213-0f30-49e2-bde9-e078b6f11657)

# Step3: Create S3 Bucket (My S3 Bucket name :supermariombk)
![image](https://github.com/user-attachments/assets/233804e7-32d0-42fa-967a-bb60d140bc5c)

# Step4 : Security Group with port access
![image](https://github.com/user-attachments/assets/7f9fdd36-8406-4265-a9b5-c9c30939c01d)

# Step 5: Clone the below repo:
git clone https://github.com/MBkalpana/K8S-Super-Mario.git

# Step 6 :

cd k8s-mario

sudo chmod +x script.sh
./script.sh

This script will install Terraform, AWS cli, Kubectl, Docker.

# Check the versions:

docker --version
aws --version
kubectl version --client
terraform --version

![image](https://github.com/user-attachments/assets/ecb87053-2db7-41a6-ba67-25ed793a980b)

Now change directory into the EKS-TF,Run Terraform init
NOTE: Don’t forgot to change the s3 bucket name in the backend.tf file

cd EKS-TF
terraform init



![image](https://github.com/user-attachments/assets/12151b56-a39f-460f-9568-9e682cbdb29f)

Now run terraform validate and terraform plan
terraform validate
terraform plan



![image](https://github.com/user-attachments/assets/3f53e2c0-9eeb-4252-b963-1ef0ee4a77ce)

Now Run terraform apply to provision cluster.


terraform apply --auto-approve


![image](https://github.com/user-attachments/assets/c0554941-f77a-4e58-80a5-b4954a245167)

Completed in 6mins

![image](https://github.com/user-attachments/assets/16c50922-8f0d-459c-8128-299c12e1836e)


![image](https://github.com/user-attachments/assets/6b32438a-d23c-4528-a7d7-61932135d6ea)


# Update the Kubernetes configuration

# Make sure change your desired region

aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1

![image](https://github.com/user-attachments/assets/d723299f-edb4-49ea-8338-48a8c1ea6c28)

kubectl describe service mario-service
![image](https://github.com/user-attachments/assets/fdca6d4f-0640-4bc1-babb-3f8d2f0a9b6c)

# Deploy the Super Mario Game

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

![image](https://github.com/user-attachments/assets/d1ff33e5-45a0-4090-803f-f5f3b57970de)

Access the Game: 

kubectl get svc mario-service

Paste the Load balancer ingress link in a browser and you will see the Mario game.

![Screenshot 2025-01-15 091945](https://github.com/user-attachments/assets/6b499fc0-be8c-40cb-b6ea-25b21f38405e)


**Directory Structure:**



![Directory structure](https://github.com/user-attachments/assets/e3b5ed34-1de7-4d74-96ca-d6ee8a8050e6)


# Destruction :

Let’s remove the service and deployment first

kubectl get all
kubectl delete service mario-service
kubectl delete deployment mario-deployment

# Let’s Destroy the cluster:

terraform destroy --auto-approve


# Note: Make sure to destroy all the resources once after deployment inorder to reduce the cost.



































