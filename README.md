# 🚜 AWS Docker Infrastructure


### Terraform Modules:
1. [ecr-infra](./fargate/ecr-infra)
2. [ecs-infra](./fargate/ecs-infra)
3. [codepipeline](./fargate/codepipeline)

> ✏️ See the tutorial [here](./fargate/README.md)

### How to setup:
- Create the IAM user and apply the required permissions
- Generate the AWS CLI access keys in the IAM console
- Install and configure the AWS CLI
- Configure the [Codestar Connection](https://docs.aws.amazon.com/codepipeline/latest/userguide/connections-github.html)
- Clone the repository
- Rename the repository folder to the application name: `mv <REPO> <APP>`
- `cd <APP>/fargate/<MODULE>/`



#### Modify the AWS provider block
- Located in the "`main.tf`" file in each module
- _Option 1_ - Add the AWS access and secret keys:
```sh
# provider "aws" {
    access_key = "*****"
    secret_key = "*****"
# }
```
- _Option 2_ - Configure an additional AWS CLI profile:
```sh
# provider "aws" {
    profile = "test"
# }
```
- _Option 3_ - Set the AWS environment variables in the terminal and omit the values from the provider:
```sh
export AWS_ACCESS_KEY_ID=*****
export AWS_SECRET_ACCESS_KEY=*****
export AWS_SESSION_TOKEN=*****
```
- _Option 4_ - Use SSO with with IAM Identity Center


#### Set the variables
- _Option 1_ - Add a "`terraform.tfvars`" file in each module directory:
```sh
aws_region="eu-west-2"
app_name="nodejs-express"
app_port=3000
app_count=1
...
```
- _Option 2_ - Set the default variables directly in the "`variables.tf`" file


### 🚀 How to run the module:
```sh
terraform init
terraform plan
terraform apply
```

### ☁️ AWS Resources:
- [x] **Virtual Private Cloud** (VPC)
    - Subnets
    - Internet Gateway
    - Route Tables
    - NAT Gateway
- [x] **Application Load Balancer** (ALB)
    - ALB HTTP Listener
    - ALB Listener Rules
    - Target Groups
    - Target Group Health Checks
- [ ] **IAM Roles & Policies**
- [x] **Security Groups**
- [x] **Systems Manager Parameter Store** (SSM)
- [x] **Elastic Container Registry** (ECR)
- [x] **Elastic Container Service** (ECS)
    - ECS Cluster
    - ECS Task Definition
    - ECS Service
- [x] **CodePipeline**
- [x] **CodeBuild**
- [x] **CodeDeploy**
- [X] **S3 Bucket Artifacts**

### 💡 Features
- [ ] Refactor the monolithic Terraform configuration
- [ ] Migrate the local state to a remote S3 backend
- [ ] Lock and upgrade the [provider versions](https://developer.hashicorp.com/terraform/tutorials/configuration-language/provider-versioning)
- [ ] Terraform one-click deployments
