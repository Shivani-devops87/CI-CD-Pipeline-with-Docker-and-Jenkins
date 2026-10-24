# CI/CD Pipeline for Microservices on AWS (EKS)

**Author:** devopsbydhairyashil

## Overview
This repository demonstrates an advanced, scripted Jenkins CI/CD pipeline that builds a Docker image for a simple Flask microservice, pushes it to DockerHub (placeholder `dhairyashil`), and deploys to Amazon EKS using Kubernetes manifests. Terraform configuration is included as an optional example to create VPC and EKS resources in `ap-south-1` (Mumbai).

## What is included
- `app/` - Simple Flask app, Dockerfile, requirements
- `kubernetes/` - Deployment and Service manifests
- `terraform/` - Example Terraform code for VPC + EKS (optional)
- `Jenkinsfile` - Scripted (advanced) Jenkins pipeline
- `README.md` - This file

## How to use
1. **Clone the repo**
   ```bash
   git clone https://github.com/devopsbydhairyashil/ci-cd-pipeline-aws.git
   cd ci-cd-pipeline-aws
   ```

2. **Build and run locally**
   ```bash
   cd app
   docker build -t dhairyashil/flask-app:local .
   docker run --rm -p 5000:5000 dhairyashil/flask-app:local
   ```

3. **(Optional) Create AWS infra with Terraform**
   - Edit `terraform/variables.tf` if you need to change `aws_region` or `cluster_name`.
   - Initialize & apply:
   ```bash
   cd terraform
   terraform init
   terraform apply
   ```
   **Warning:** Terraform will create real AWS resources which may incur charges. Only run if you understand the cost.

4. **Jenkins configuration**
   - Create a Jenkins job using the provided `Jenkinsfile`.
   - Add credentials in Jenkins:
     - `dockerhub-creds` (Username & Password) — DockerHub account
     - `kubeconfig` (Secret text) — kubeconfig content from Terraform/module or your cluster
   - Ensure Jenkins agents have Docker and kubectl installed, or run Docker build/push on an agent that supports it.

5. **Customize**
   Replace the placeholder DockerHub username `dhairyashil` with your DockerHub account if desired. The pipeline tags images with the Jenkins `$BUILD_NUMBER`.

## Notes & Recommendations
- Kubernetes manifests use `dhairyashil/flask-app` as the image. Change it if you push to a different repo.
- Store sensitive data (kubeconfig, DockerHub creds) as Jenkins credentials.
- The Terraform module versions and configs are examples — adjust to your organization policies.

## Author
Dhairyashil (GitHub: devopsbydhairyashil)
