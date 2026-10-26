# Terraform + Docker: Nginx Container Deployment

## Project Overview

This project demonstrates **Infrastructure as Code (IaC)** using Terraform to provision and manage a Docker container running the Nginx web server.

Terraform automates the creation, configuration, verification, and removal of Docker resources, reducing the need for manual container management.

## Objectives

- Understand Infrastructure as Code using Terraform.
- Configure the Docker provider.
- Download and manage a Docker image.
- Deploy an Nginx container using Terraform.
- Preview infrastructure changes using `terraform plan`.
- Inspect managed resources using Terraform state commands.
- Destroy resources using `terraform destroy`.

## Technologies Used

- **Terraform** — Infrastructure provisioning and lifecycle management
- **Docker** — Container runtime
- **Nginx** — Web server
- **Ubuntu on WSL** — Development environment
- **Git and GitHub** — Version control and project hosting
- **HCL** — Terraform configuration language

## Architecture

```text
Terraform Configuration (main.tf)
              |
              v
       Terraform CLI
              |
              v
       Docker Provider
              |
       +------+------+
       |             |
       v             v
  Nginx Image    Docker Container
                     |
                     v
               Host Port 8082
                     |
                     v
              Nginx Welcome Page
```

## Project Structure

```text
terraform-docker-project/
├── main.tf
├── .terraform.lock.hcl
├── .gitignore
└── README.md
```

## Configuration

The `main.tf` file defines the Docker provider, the `nginx:alpine` image, and a container named `terraform-nginx`.

The container maps port **80 inside the container** to port **8082 on the host**.

Port 8082 is used to avoid the existing Jenkins service on port 8080.

## Prerequisites

- Docker Desktop installed and running
- Docker integration enabled for your WSL Ubuntu distribution
- Terraform installed
- Git installed
- A terminal with access to Docker

Verify the installations:

```bash
terraform -version
docker --version
docker info
git --version
```

## Deployment Steps

### 1. Initialize Terraform

```bash
terraform init
```

Initializes the working directory and installs the required Docker provider.

### 2. Format the configuration

```bash
terraform fmt
```

Formats the Terraform configuration according to standard HCL formatting.

### 3. Validate the configuration

```bash
terraform validate
```

Checks the configuration for syntax and structural errors.

### 4. Preview the changes

```bash
terraform plan
```

Shows the resources Terraform intends to create or modify before applying changes.

### 5. Create the infrastructure

```bash
terraform apply
```

Review the plan and enter `yes` when prompted.

### 6. Verify the running container

```bash
docker ps
```

Check the Nginx response:

```bash
curl -I http://localhost:8082
```

A successful response should contain `HTTP/1.1 200 OK` and an Nginx server header.

Open the application in your browser:

http://localhost:8082

The Nginx welcome page confirms that the web server is accessible.

## Terraform State Management

List the resources managed by Terraform:

```bash
terraform state list
```

Inspect the container resource:

```bash
terraform state show docker_container.nginx
```

## Resource Cleanup

Preview the resources that will be destroyed:

```bash
terraform plan -destroy
```

Remove the Terraform-managed container and image:

```bash
terraform destroy
```

Enter `yes` when prompted.

Verify that the managed resources have been removed:

```bash
terraform state list
docker ps
```

The Terraform state should contain no managed resources after destruction. Other Docker containers not managed by this configuration should remain unaffected.

## Important Notes

- Run Terraform commands from the project directory.
- Ensure Docker Desktop is running before using the Docker provider.
- Do not commit Terraform state files or the `.terraform` directory.
- Keep `.terraform.lock.hcl` under version control to record the selected provider version.
- Terraform state can contain sensitive information; keep it out of public repositories.

## Learning Outcomes

- Implemented Infrastructure as Code with Terraform.
- Used the Docker provider to manage a container and image.
- Practiced the Terraform `init`, `fmt`, `validate`, `plan`, `apply`, `state`, and `destroy` workflow.
- Verified a deployed Nginx web server.
- Published the configuration to GitHub.

## Author

**Ruchita Durgade**

GitHub: https://github.com/ruchi1792

---

*This project was created for hands-on learning and practice with Terraform, Docker, and Infrastructure as Code.*
