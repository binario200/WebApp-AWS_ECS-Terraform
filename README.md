# Web Application deployment to AWS using Terraform, AWS ECS and Fargate

Terraform configurations to deploy a docker web app using ECS and Fargate.

Also Terraform will deploy:

- VPC with 4 subnets (2 public and 2 private) in each Availability Zone.
- A NAT to allow the private network access the internet.
- A Application load balancer (ALB)
- EC2 cluster
- Task and a Service to deploy the Web Application and its Database to ECS
- Auto-scaling configuration
- A Pipeline to deploy the app using AWS CodePipeline, CodeBuilde, ECR to store docker images.
- A S3 Bucket
- A Web Application running in a docker container.
- A Database using AWS RDS

## Terraform Project infrastructure
```
├── modules
│ └── code_pipeline
│ └── ecs
│ └── networking
│ └── rds
| └── S3
├── prod
  └── data-stores
    └── postgresql
      └── main.tf
      └── outputs.tf
      └── vars.tf      
  └── services
    └── webapp-cluser
      └── main.tf
      └── outputs.tf
      └── vars.tf    
├── stage
  └── data-stores
    └── postgresql
      └── main.tf
      └── outputs.tf
      └── vars.tf
  └── services
    └── webapp-cluser
      └── main.tf
      └── outputs.tf
      └── vars.tf
```

## Requeriments
In order to try these configurations and deploy this infrastructure at AWS

- An AWS account (with the permissions to: )
- Terraform
- Github Account

## AWS ECS Terminology

- Cluster: It is a group of EC2 instances hosting containers.
- Task definition: It is the specification of how ECS should run your app. Here you define which image to use, port mapping, memory, environments variables, etc.
- Service: Services launches and maintains tasks running inside the cluster. A Service will auto-recover any stopped tasks keeping the number of tasks running as you specified.
- Fargate is a technology that allows running containers in ECS without needing to manage the EC2 servers for cluster. You only deploy your Docker applications and set the scaling rules for it. Fargate is an execution method from ECS.
