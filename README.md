# Complete Project Guide

## 1. Infrastructure Setup (Terraform)

### AWS Configuration
 
# Install AWS CLI
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi

# Verify Installation
aws --version

# Configure AWS
aws configure
# AWS Access Key ID: 
# AWS Secret Access Key: 
# Default region name: ue-west-2
# Default output format: json
 

### Terraform Commands
 
# Initialize Terraform
terraform init

# Plan Infrastructure
terraform plan

# Apply Infrastructure
terraform apply
 

## 2. Helm Deployment

### Installation & Setup
 
# Install Helm
winget install Helm.Helm

# Create Helm Chart
helm create laravel-helm-app

# Package Chart
helm package laravel-helm-app

# Configure EKS Context
aws eks update-kubeconfig --name laravel-cluster --region eu-west-2
 

### Deployment Commands
 
# Install Application
helm install laravel-helm-app ./laravel-helm-app-0.1.0.tgz

helm install laravel-helm-app ./laravel-helm-app-0.1.0.tgz --set service.type=LoadBalancer

# Uninstall Application
helm uninstall laravel-helm-app

# Verify Deployment
kubectl get pods
kubectl get svc
 

## 3. Local Development

### Setup Commands
 
# Clone Repository
git clone https://gitlab.com/inno2582320/laravel-10-boilerplate-task.git
cd laravel-10-boilerplate-task

# Start Docker Environment
docker-compose up -d

# Initialize Laravel
docker-compose exec app composer install
docker-compose exec app php artisan key:generate
docker-compose exec app php artisan migrate
 

# Project Structure

laravel-10-boilerplate-task/
├── Application Core
│   ├── app/                          # Core application code
│   │   ├── Console/                  # Console commands
│   │   ├── Http/                     # HTTP layer (Controllers, Middleware)
│   │   ├── Models/                   # Database models
│   │   └── Providers/               # Service providers
│   
├── Infrastructure
│   ├── terraform/                    # Infrastructure as Code
│   │   ├── modules/
│   │   │   ├── ecr/                 # ECR repository module
│   │   │   ├── eks/                 # EKS cluster module
│   │   │   └── vpc/                 # VPC network module
│   │   └── main.tf                  # Main terraform configuration
│   
├── Kubernetes Deployment
│   └── laravel-help-app/            # Helm chart directory
│       ├── templates/               # Kubernetes manifest templates
│       ├── Chart.yaml              # Chart definition
│       └── values.yaml             # Configuration values
│   
├── Local Development
│   └── dev/
│       └── docker-compose/         # Local development containers
│           ├── mysql/              # MySQL configuration
│           ├── nginx/              # Nginx configuration
│           ├── php/                # PHP configuration
│           └── redis/              # Redis configuration
│   
├── CI/CD
│   └── .gitlab-ci.yml              # GitLab CI/CD configuration
│   
└── Laravel Framework Files
    ├── config/                     # Application configuration
    ├── database/                   # Database migrations & seeds
    ├── resources/                  # Frontend resources
    ├── routes/                     # Application routes
    └── tests/                      # Test files

## Important Configuration Notes

### GitLab Branch Protection
Settings -> Repository -> Protected Branches
main:
  - Allowed to push: No one
  - Allowed to merge: Maintainers
  - Require pipeline to succeed: Yes
 

### Helm Values Configuration
# values.yaml
service:
  type: LoadBalancer
  port: 80
 

### IAM User Setup
- Created user: "evaluator-user"
- Permissions: 
  - EKS access
  - ECR access

