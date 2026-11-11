# WordPress Deployment on Kubernetes with AWS Persistent Storage

## 📌 Project Overview

This project demonstrates deploying a WordPress application with a MySQL database on a Kubernetes cluster, using AWS storage services for persistent data management.

The architecture separates application files from database storage using AWS EFS and EBS, ensuring data persistence even when Pods are restarted or recreated.

## 🏗️ Architecture

![Project Architecture](architecture.png)

### Architecture Components

**1. Kubernetes Deployments**
- WordPress Deployment
- MySQL Deployment

**2. Kubernetes Services**
- WordPress Service
- MySQL Service

**3. Kubernetes Storage**
- Persistent Volumes (PV)
- Persistent Volume Claims (PVC)

**4. AWS Storage Integration**
- Amazon EBS for MySQL database persistence.
- Amazon EFS for WordPress shared file storage.

**5. Kubernetes Secrets**
- Store MySQL credentials securely.
- Pass database configuration to WordPress.

## 💾 Storage Architecture

### Amazon EBS – MySQL

EBS provides block-level storage for the MySQL database.

It stores:
- User accounts and credentials.
- Posts and pages.
- Comments and website settings.
- Database tables and records.

### Amazon EFS – WordPress

EFS provides shared network file storage for WordPress.

It stores:
- Uploaded images and media files.
- WordPress themes.
- Plugins.
- Shared application files.

**Why use both?**

EBS is suitable for database block storage, while EFS allows multiple WordPress Pods to access shared files simultaneously.

## 🔄 Application Workflow

1. Users access the WordPress application through its Kubernetes Service.
2. WordPress communicates with MySQL through the internal MySQL Service.
3. MySQL reads and writes database information on its EBS-backed Persistent Volume.
4. WordPress stores uploaded media and shared files on its EFS-backed Persistent Volume.
5. Kubernetes manages the application Pods and their persistent storage.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Kubernetes | Container orchestration |
| WordPress | Content Management System |
| MySQL | Relational Database |
| AWS EBS | Persistent block storage |
| AWS EFS | Shared file storage |
| PV & PVC | Kubernetes storage management |
| Kubernetes Secrets | Credential management |

## 📂 Repository Structure

```text
.
├── mysql/
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   ├── mysql-pv.yaml
│   └── mysql-pvc.yaml
│
├── wordpress/
│   ├── wordpress-deployment.yaml
│   ├── wordpress-service.yaml
│   ├── wordpress-pv.yaml
│   └── wordpress-pvc.yaml
│
├── secrets/
│   └── mysql-secret.yaml
│
├── architecture.png
└── README.md
```

*Note: Adjust the directory structure to match the actual YAML files in your repository.*

## ⚙️ Prerequisites

Before deploying the application, make sure you have:

- A running Kubernetes cluster.
- AWS account with the required permissions.
- AWS EBS CSI Driver.
- AWS EFS CSI Driver.
- An EBS volume and EFS file system configured.
- kubectl installed and configured.

## 🚀 Deployment

Apply the Kubernetes manifests:

```bash
# Create MySQL credentials
kubectl apply -f secrets/

# Deploy MySQL resources
kubectl apply -f mysql/

# Deploy WordPress resources
kubectl apply -f wordpress/
```

Check the deployed resources:

```bash
kubectl get pods
kubectl get services
kubectl get pv
kubectl get pvc
```

## 🎯 Key Learning Outcomes

- Deploying stateful applications on Kubernetes.
- Managing persistent storage using PVs and PVCs.
- Integrating Kubernetes with AWS EBS and EFS.
- Understanding the differences between block and shared file storage.
- Managing application credentials using Kubernetes Secrets.
- Understanding storage requirements for multi-Pod applications.

---

**Author:** Bassem Osama

**Focus:** DevOps | Kubernetes | AWS | Cloud Infrastructure
```
