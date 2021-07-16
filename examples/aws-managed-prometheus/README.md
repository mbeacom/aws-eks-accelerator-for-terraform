# AWS Managed Prometheus(AMP) and AWS Managed Grafana (AMG)

This document walk-through the process of deploying end to end AWS managed Prometheus and Grafana solution in AWS CLoud using Terraform 

The following components gets deployed as part of this solution

   - AWS VPC, Public and Private subnets, Internet gateway and NAT Gateway
   - Creates AWS EKS Cluster with multiple managed node groups(worker nodes)
   - Deploy Prometheus Server in EKS Cluster using Helm Provider
   - Create AWS Managed Prometheus Workspace(AMP) to collect the metrics from EKS Cluster
   - Create necessary IAM roles for AWS Managed Prometheus Workspace(AMP)
   - Configure remote write metrics from Prometheus Server to AWS Managed Prometheus Workspace(AMP)
   - Create VPC Endpoints for AWS Managed Prometheus Workspace to communicate securely from Private subnets
   - Create AWS Managed Grafana Workspace (Using AWS Console only. No Terraform at this moment)
   - Add AWS Managed Prometheus data source to Grafana and query the metrics

# Architecture


# Deploying the Solution

## Step1: Clone this repo

```shell script
git clone https://github.com/aws-samples/aws-eks-accelerator-for-terraform.git
```

## Step2: Copy Prometheus configuration file to live folder under dev cluster

This step replaces the `aws-managed-prometheus.tfvars` config with Dev `base.tfvars`

 ```shell script
 cp examples/aws-managed-prometheus/aws-managed-prometheus.tfvars live/preprod/eu-west-1/application/dev/base.tfvars
 ```

## Step2: Clone this repo


## Step2: Clone this repo


## Step2: Clone this repo


# Summary


