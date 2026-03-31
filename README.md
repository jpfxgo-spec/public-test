# Amazon EKS Cluster Terraform Deployment

This repository contains Terraform configuration to deploy a basic Amazon EKS (Elastic Kubernetes Service) cluster.

## Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) (>= 1.0)
- [AWS CLI](https://aws.amazon.com/cli/) configured with appropriate credentials
- [kubectl](https://kubernetes.io/docs/tasks/tools/) (optional, for interacting with the cluster)

## Quick Start

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd public-test
   ```

2. Initialize Terraform:
   ```bash
   terraform init
   ```

3. Review the plan:
   ```bash
   terraform plan
   ```

4. Apply the configuration:
   ```bash
   terraform apply
   ```

5. Configure kubectl (optional):
   ```bash
   aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)
   ```

## Configuration

The deployment includes:
- VPC with public and private subnets
- EKS cluster with managed node group
- IAM roles and policies for EKS and worker nodes
- NAT gateways for private subnet internet access

### Variables

You can customize the deployment by modifying variables in `variables.tf` or creating a `terraform.tfvars` file:

- `region`: AWS region (default: us-east-1)
- `cluster_name`: Name of the EKS cluster (default: my-eks-cluster)
- `cluster_version`: Kubernetes version (default: 1.28)
- `vpc_cidr`: VPC CIDR block (default: 10.0.0.0/16)
- `public_subnets`: List of public subnet CIDRs
- `private_subnets`: List of private subnet CIDRs
- `node_instance_type`: EC2 instance type for nodes (default: t3.medium)
- `node_desired_capacity`: Desired number of nodes (default: 2)

## Cleanup

To destroy the resources:
```bash
terraform destroy
```

## Security Note

This is a basic configuration for demonstration purposes. For production use, consider:
- Using private subnets for worker nodes
- Implementing proper security groups
- Adding logging and monitoring
- Using AWS KMS for encryption
- Implementing backup strategies