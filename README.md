# Homework Assignment: Terraform to HCP

This repository contains a Terraform configuration designed to deploy infrastructure on HashiCorp Cloud Platform (HCP). The configuration includes the setup of virtual private clouds (VPCs), subnets, internet gateways, NAT gateways, route tables, security groups, load balancers, auto-scaling groups, and EC2 instances.

## Prerequisites

Before using this Terraform configuration, ensure you have the following:

- [Terraform](https://www.terraform.io/downloads.html) installed.
- AWS credentials configured in your environment.
- Access to HashiCorp Cloud Platform (HCP).

## Repository Structure

The repository is organized as follows:

- **Authentication and Configuration Files:**
  - `0-Auth.tf`: Manages authentication configurations.
  - `.gitignore`: Specifies files and directories to be ignored by Git.

- **Network Infrastructure:**
  - `1-VPC.tf`: Defines the Virtual Private Cloud.
  - `2-Subnets.tf`: Configures subnets within the VPC.
  - `3-IGW.tf`: Sets up the Internet Gateway.
  - `4-NAT.tf`: Configures the NAT Gateway.
  - `5-Route.tf`: Manages route tables and routes.

- **Security Groups:**
  - `6-SG-All.tf`: Defines security groups for the infrastructure.

- **Compute Resources:**
  - `10.LaunchTemplate.tf`: Creates launch templates for EC2 instances.
  - `8-AutoScalingGroup.tf`: Sets up auto-scaling groups for EC2 instances.
  - `13-ubuntu.tf`: Configures Ubuntu-based EC2 instances.

- **Load Balancing:**
  - `9-TargetGroup.tf`: Defines target groups for load balancing.
  - `7-LoadBalancer.tf`: Configures the load balancer.

- **Domain Name System (DNS):**
  - `11.Route53.tf`: Manages Route 53 configurations for DNS.

- **Key Management:**
  - `12.Key.tf`: Manages SSH key pairs for accessing EC2 instances.

- **Scripts:**
  - `ec2scrpit.sh`: Shell script related to EC2 instances.
  - `japanscrpit.sh`: Shell script related to specific configurations (possibly region-specific).

- **GitHub Workflow and CI/CD:**
  - `.github/workflows/`: Contains GitHub Actions YAML configuration files for automated deployments and testing.
    - `.github/workflows/terraform-apply.yml`: Automates the application of Terraform configurations, provisioning the infrastructure.
    - `.github/workflows/terraform-plan.yml`: Generates and reviews Terraform execution plans before applying changes.
  - `.github/ISSUE_TEMPLATE/`: Templates for reporting issues and feature requests.
  - `.github/PULL_REQUEST_TEMPLATE.md`: Provides a structured template for pull request submissions.

## Creating a Pipeline on HCP Terraform

To set up a Terraform pipeline in HashiCorp Cloud Platform (HCP):

1. **Access Terraform Cloud:**
   - Navigate to [Terraform Cloud](https://app.terraform.io/app/organizations).
   - Log in with your credentials.

2. **Create a New Organization:**
   - Click on "New Organization" if you have not already created one.
   - Set the organization name as `TIQS`.
   - Configure settings as required.

3. **Create a New Workspace:**
   - Go to "Workspaces" and click "New Workspace".
   - Choose "Version Control Workflow" and connect your GitHub repository.
   - Select the `homework-assignment-terraform-to-hcp` repository.
   - Name the workspace appropriately (e.g., `terraform-hcp-pipeline`).

4. **Configure Variables:**
   - Navigate to "Variables" in the workspace.
   - Add the necessary environment variables:
     - `AWS_ACCESS_KEY_ID`
     - `AWS_SECRET_ACCESS_KEY`

5. **Enable the Pipeline:**
   - Push changes to your GitHub repository.
   - The `.github/workflows/terraform-apply.yml` and `.github/workflows/terraform-plan.yml` will trigger the pipeline.
   - Monitor the Terraform runs in the Terraform Cloud UI.

6. **Review and Apply Changes:**
   - Navigate to the "Runs" tab in your Terraform Cloud workspace.
   - Review the execution plan and approve the run.
   - Terraform will provision resources as defined in the `.tf` files.

7. **Monitor and Manage Infrastructure:**
   - Use Terraform Cloud UI to manage state and logs.
   - Adjust workspace settings as needed.

## Usage

To deploy the infrastructure:

1. **Initialize Terraform:**

   ```bash
   terraform init
   ```

2. **Review the Execution Plan:**

   ```bash
   terraform plan
   ```

3. **Apply the Configuration:**

   ```bash
   terraform apply
   ```

   Confirm the apply step when prompted.

4. **Destroy the Infrastructure (if needed):**

   ```bash
   terraform destroy
   ```

   Confirm the destroy step when prompted.

## Notes

- Ensure that all necessary variables are defined before applying the configuration.
- Review and customize the configuration files as needed to fit your specific requirements.

For more details, refer to the individual `.tf` files in this repository.
