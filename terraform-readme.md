# 🚀 Creating EKS, VPC & Remote Backend Resources on AWS using Terraform


---

## 📖 Overview  
This repository contains **Infrastructure as Code (IaC)** for deploying the **Ultimate DevOps Project Demo** application on AWS.  
It provisions S3, DynamoDB, EKS Cluster and VPC.


---

## 📦 What’s Included  

## 🗄️ S3 storing state file
- Stores Terraform state remotely in an S3 bucket for better collaboration.

## 🔒 DynamoDB for state locking
- State locking to avoid race conditions while applying changes.
- Ensures safe parallel execution of Terraform.

## ☸️ EKS
- Creates an Amazon EKS cluster for secure deployment.

## 🌐 VPC
- Creates a secure VPC with network isolation using public/private subnets, route tables, and network connections.



---

## 🏗️ Project Structure  

```bash
Terraform/
│── main.tf               # Root module: entry point for Terraform execution
│── variables.tf          # Input variable definitions for the root module
│── outputs.tf            # Output values from the root module
│
├── backend/              # Backend configuration & state management
│   ├── main.tf           # Defines backend (S3 + DynamoDB for state & locking)
│   ├── outputs.tf        # Backend-related outputs
│   ├── terraform.tfstate # Current Terraform state file
│   ├── terraform.tfstate.backup # Backup of the state file
│
├── modules/              # Reusable infrastructure modules
│   │
│   ├── eks/              # Amazon EKS (Kubernetes) module
│   │   ├── main.tf       # Resources for EKS cluster (nodes, roles, etc.)
│   │   ├── variables.tf  # Inputs required for EKS
│   │   ├── outputs.tf    # Outputs from EKS (endpoint, kubeconfig)
│   │
│   └── vpc/              # Amazon VPC networking module
│       ├── main.tf       # Resources for VPC (subnets, IGW, NAT, etc.)
│       ├── variables.tf  # Inputs required for VPC
│       ├── outputs.tf    # Outputs from VPC (VPC ID, subnet IDs)

```

## ⚙️ Prerequisites
- AWS account with programmatic access (IAM user/role).
- Terraform installed locally.
- AWS CLI installed and configured.
- Sufficient permissions to create S3, DynamoDB, VPC, and EKS resources.

## 🚀 Setup AWS CLI
1) Install and configure AWS CLI to allow Terraform to access AWS APIs.  
Official documentation: [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html#getting-started-install-instructions)



2) Install unzip (required for some AWS CLI packages):  
   ```
   sudo apt install unzip
   ```

3) Verify AWS CLI installation:  
   ```
   aws --version
   ```
   <img width="647" height="148" alt="image" src="https://github.com/user-attachments/assets/5c8d42fc-404f-48f4-95fc-941ad85289a6" />


5) Configure AWS credentials and defaults:  
   ```
   aws configure
   ```
   Provide: AWS Access Key ID, AWS Secret Access Key, Default region name, Default output format.

7) Verify configuration:  
   ```
   aws configure list
   ```
<img width="601" height="120" alt="image" src="https://github.com/user-attachments/assets/7c4d895d-5ef1-4677-8893-bc95c593748b" />

## 🧭 Initialize Remote Backend (S3 + DynamoDB)
1) Clone the repository containing your Terraform code and go to that directory:  
   ```
   git clone https://github.com/I-am-nk/ultimate-devops-project-terraform.git
   ```

2) Change directory to the backend folder (where backend config is stored).
   ```
   cd backend
   ```
<img width="949" height="93" alt="image" src="https://github.com/user-attachments/assets/c17902b2-e398-4623-96fd-eb66a11bb56e" />

3) Initialize Terraform:  
  ```
terraform init
   ```
<img width="1292" height="583" alt="image" src="https://github.com/user-attachments/assets/13629d88-15d4-4afc-b1d6-cfba1a748059" />


4) Review the plan:  
   ```
   terraform plan
   ```
<img width="1600" height="769" alt="image" src="https://github.com/user-attachments/assets/ce518c9e-f103-445c-aa50-6c3ab822e170" />

5) Apply to create backend resources (S3 and DynamoDB):  
```
terraform apply
```


6) Approve when prompted with “yes.” Terraform will start creating resources.
<img width="964" height="156" alt="image" src="https://github.com/user-attachments/assets/e557ee42-c207-4cdc-9f8b-5e494cbdb5f9" />

## ✅ Verify Backend Resources
7) Verify S3 bucket creation in the AWS Console.
    <img width="1918" height="654" alt="image" src="https://github.com/user-attachments/assets/fcf21f20-62cf-47c5-98d3-8b4630641311" />

8) Verify DynamoDB table creation in the AWS Console.
    <img width="1919" height="539" alt="image" src="https://github.com/user-attachments/assets/0ef83e62-a53e-4c95-af11-5f8f51c20fea" />


## ☸️ Create EKS and VPC
1) Change directory to the main Terraform folder (project root, e.g., /Terraform).

2) Initialize Terraform:  
    ```
     terraform init
   ```

3) Review the execution plan:  
   ```
       terraform plan
   ```
4) Apply to provision EKS and VPC:  
   ```
    terraform apply
   ```
5) Approve when prompted to proceed.

## 🔍 Verify EKS and VPC
6) Confirm the EKS cluster is created in the AWS Console.
<img width="798" height="200" alt="1" src="https://github.com/user-attachments/assets/34b238db-093f-4f39-a1ed-1bf4d5b96b08" />

19) Confirm the VPC and networking components are created (VPC, subnets, route tables, IGW/NAT). +
<img width="799" height="358" alt="2 " src="https://github.com/user-attachments/assets/02e57b4a-0ea2-4a52-a0b2-5d911c397eff" />


## 🧹 Cleanup
To destroy all infrastructure and avoid ongoing charges:  
```
    terraform destroy
```



