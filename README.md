# Launch-Kubernetes-Clusters-with-Amazon-EKS

## Project Overview
This project walks you through deploying your first Kubernetes cluster using **Amazon Elastic Kubernetes Service (EKS)**. You’ll learn to use **eksctl**, manage IAM roles, track resources with **CloudFormation**, and test the self-healing capabilities of a Kubernetes cluster.

## Prerequisites
Before you start, ensure you have the following:
- An **AWS account**.
- Basic knowledge of **AWS services**, such as **EC2**, **IAM**, and **CloudFormation**.
- **AWS CLI** installed and configured on your local machine.
- **eksctl** installed on your EC2 instance (or local machine).

## Steps to Complete the Project

### 1. Launch and Connect to an EC2 Instance
- Launch an EC2 instance that will serve as your workspace for creating the EKS cluster.
- Set up the security group for SSH access.

### 2. Install **eksctl**
Use the following commands to install **eksctl** on your EC2 instance:

curl --silent --location "https://github.com/weaveworks/eksctl/releases/download/v0.65.0/eksctl_Linux_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin

3. Create a Kubernetes Cluster Using eksctl
Run the following command to create a Kubernetes cluster:

Copy code
eksctl create cluster \
--name eks-cluster \
--nodegroup-name nextwork-nodegroup \
--node-type t2.micro \
--nodes 3 \
--nodes-min 1 \
--nodes-max 3 \
--version 1.21 \
--region us-east-1

4. Set IAM Permissions for Access
Ensure you have the correct IAM roles and policies to manage the cluster. You can configure these using the AWS Management Console or CLI.

5. Track Cluster Creation Using CloudFormation
eksctl uses CloudFormation behind the scenes to create resources such as VPCs and security groups. Monitor the CloudFormation stack for cluster and node group creation.

6. Verify the Cluster
Once the cluster is created, use kubectl to verify the nodes:

Copy code
kubectl get nodes

7. Test Cluster Resilience
Delete a node in the EC2 console and watch Kubernetes automatically recreate the node to maintain the desired cluster state.

##Costs and Cleanup
* EKS is not Free Tier eligible. Be aware that there is a cost of $0.10 USD/hour for each running EKS cluster.
* Make sure to delete all resources when done to minimize costs.
Run the following command to delete your cluster:

eksctl delete cluster --name eks-cluster

##Conclusion
In this project, you learned how to set up and manage an EKS Kubernetes cluster on AWS. You used eksctl for quick setup, managed IAM permissions, tracked resources with CloudFormation, and observed Kubernetes’ self-healing capabilities.


---

### Key Sections in the README:
1. **Project Overview**: A brief description of the project and its purpose.
2. **Prerequisites**: Lists what needs to be set up before starting.
3. **Steps to Complete the Project**: A clear, step-by-step guide on how to deploy the EKS cluster.
4. **Costs and Cleanup**: Important notes on pricing and how to clean up resources.
5. **Conclusion**: A recap of what was learned and achieved.

This **README** file helps other developers easily understand how to follow the project and set up their own Kubernetes cluster using Amazon EKS.
