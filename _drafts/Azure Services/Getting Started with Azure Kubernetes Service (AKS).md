# Getting Started with Azure Kubernetes Service (AKS)

## Introduction

Azure Kubernetes Service (AKS) simplifies deploying, managing, and scaling containerized applications using Kubernetes. In this guide, we’ll walk you through setting up your first AKS cluster and deploying a sample application.

## Prerequisites

- An active Azure account
- Basic understanding of Kubernetes concepts
- Azure CLI installed on your local machine

## Step 1: Create an AKS Cluster

1. Open the Azure Portal and navigate to `Kubernetes services`.
2. Click `Add` to create a new Kubernetes cluster.
3. Fill in the necessary details:
   - **Resource group**: Create a new or select an existing one.
   - **Kubernetes cluster name**: Enter a unique name.
   - **Region**: Choose your preferred region.
   - **Node size and count**: Select the appropriate VM size and node count for your workload.
4. Click `Review + create`, then `Create` to provision the cluster.

## Step 2: Configure kubectl

1. Once the cluster is created, open the Azure CLI or Cloud Shell.
2. Run the following command to configure `kubectl` to connect to your AKS cluster:
   ```sh
   az aks get-credentials --resource-group <YourResourceGroup> --name <YourAKSClusterName>
   ```
3. Verify the connection by running:
   ```sh
   kubectl get nodes
   ```

## Step 3: Deploy a Sample Application

1. Create a deployment YAML file (`deployment.yaml`) with the following content:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         labels:
           app: nginx
       spec:
         containers:
           - name: nginx
             image: nginx:1.14.2
             ports:
               - containerPort: 80
   ```
2. Apply the deployment:
   ```sh
   kubectl apply -f deployment.yaml
   ```
3. Verify the deployment:
   ```sh
   kubectl get deployments
   ```

## Step 4: Expose the Application

1. Create a service YAML file (`service.yaml`) with the following content:
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-service
   spec:
     selector:
       app: nginx
     ports:
       - protocol: TCP
         port: 80
         targetPort: 80
     type: LoadBalancer
   ```
2. Apply the service:
   ```sh
   kubectl apply -f service.yaml
   ```
3. Get the external IP of the service:
   ```sh
   kubectl get services
   ```

## Summary

Congratulations! You've successfully set up an AKS cluster and deployed a sample application. AKS takes care of much of the complexity involved in managing Kubernetes, allowing you to focus on your applications.

## Call to Action

Ready to dive deeper into AKS? Check out our next article on advanced AKS configurations and best practices for managing your Kubernetes clusters.
