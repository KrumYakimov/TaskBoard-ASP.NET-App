# Task Board ASP.NET App + SQL Server Database + Terraform on Azure

## Description

This project is part of a hands-on exercise from the Containers and Cloud course at SoftUni.  
The goal is to deploy the Task Board ASP.NET Core web application with a SQL Server database to Microsoft Azure using Terraform.

## Infrastructure Overview

The Terraform configuration provisions the following resources:

- Resource Group
- App Service Plan (Linux)
- App Service for ASP.NET Core
- Azure SQL Server
- Azure SQL Database
- Firewall Rule to allow access from Azure
- Source code deployment from a public GitHub repository

## Configuration Details

- The app runs on .NET 6.0
- A connection string is set in the App Service to connect to the SQL Server
- Deployment is done via manual GitHub integration (no CI/CD)


## File Structure

- `main.tf` – defines all core infrastructure resources
- `variables.tf` – declares the required input variables
- `values.tfvars` – contains sensitive values for those variables (not included in repo)
- `outputs.tf` – outputs useful information like the App URL and IP addresses

## Deployment Instructions

Before you begin, make sure you have:

- Terraform installed
- An active Azure subscription
- Logged into Azure via `az login`

Then follow these steps:

1. Clone the repository
2. Create your own `values.tfvars` file (see section below)
3. Run:

```bash
terraform init
terraform validate
terraform apply -var-file="values.tfvars"
```

4. Wait for the deployment to complete and visit the output URL of the app

## Cleanup

To destroy the created Azure resources:

```bash
terraform destroy -var-file="values.tfvars"
```

## Security Notice and Usage Instructions

I have **excluded the `values.tfvars` file** from this repository on purpose, because it contains **sensitive data** such as:

- SQL Server administrator username and password
- Azure resource names unique to my setup

If you want to use or fork this repository, you’ll need to create your own `values.tfvars` file in the root of the project directory with content like:

```hcl
resource_group_name         = "your-resource-group"
resource_group_location     = "your-resource-group-location"
app_service_plan_name       = "your-app-service-plan"
app_service_name            = "your-app-service"
sql_server_name             = "your-sql-server"
sql_database_name           = "your-database"
sql_admin_username          = "your-admin"
sql_admin_password          = "your-strong-password"
firewall_rule_name          = "your-firewall-rule"
github_repo_url             = "https://github.com/your-username/your-repo"
```

## Final Notes

- This setup uses a random integer to generate unique resource names, which helps avoid naming conflicts in Azure
- The infrastructure follows good Terraform practices, including separation of configuration into modular files
- Feel free to customize the variables and deployment configuration for your own environment