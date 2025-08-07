 Task 3: Infrastructure as Code (IaC) with
 Terraform – Docker Container
 Objective
 Provision a local Docker container (Nginx) using Terraform as Infrastructure as Code (IaC).
 Tools Used- Terraform- Docker- Windows with Docker Desktop
 Project Structure
 terraform-docker-container/
 main.tf
 README.md
 main.tf (Terraform Configuration)
 terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0"
    }
  }
 }
 provider "docker" {
  host = "npipe:////./pipe/docker_engine"
 }
 resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
 }
 resource "docker_container" "nginx_container" {
  name  = "nginx_terraform"
  image = docker_image.nginx.name
  ports {
    internal = 80
    external = 8080
  }
 }
 Steps to Run
 1
 2
 Prerequisites- Docker Desktop installed and running- Terraform installed- Internet connection (to pull Docker image)
 Initialize Terraform
terraform init
 3
 4
 5
 6
 7
 Preview Terraform Plan
 terraform plan
 Apply Configuration
 terraform apply -auto-approve
 Verify the Setup
 docker ps
 Visit: http://localhost:8080
 Check Terraform State
 terraform state list
 Destroy the Infrastructure
 terraform destroy -auto-approve
 Common Issues (Windows)
 protocol not available → 
 Deliverables- main.tf- README.md- Execution logs (optional)
 Author
 Shivshankar Anil Gawali
 Use npipe:////./pipe/docker_engine in the provider block instead of Unix socket.
 Terraform | Docker | DevOps Intern Projects
