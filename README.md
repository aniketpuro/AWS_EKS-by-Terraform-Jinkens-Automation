# AWS_EKS-by-Terraform-Jinkens-Automation

This project is a complete setup for deploying an NGINX application on an AWS EKS cluster using Terraform and Jenkins. The project automates the installation and configuration of necessary tools, including Jenkins, Terraform, Kubernetes (kubectl), and AWS CLI.

## Prerequisites

Before you start, ensure you have the following installed on your local machine:

- **Terraform**: v1.0.0 or higher
- **AWS CLI**: v2.0 or higher
- **kubectl**: Latest stable version
- **Jenkins**: Installed on a server or local machine

## Project Structure

- **`Jenkinsfile`**: Defines the CI/CD pipeline for Jenkins.
- **`manifests/`**: Contains Kubernetes manifests.
  - **`deployment.yml`**: Defines the NGINX deployment.
  - **`service.yml`**: Defines the NGINX service (LoadBalancer).
- **`terraform/`**: Contains Terraform scripts.
  - **`eks.tf`**: EKS cluster setup.
  - **`provider.tf`**: AWS provider configuration.
  - **`vpc.tf`**: VPC setup for the EKS cluster.
- **`installer.sh`**: Shell script to install necessary tools (Jenkins, Terraform, kubectl, AWS CLI).

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/yeshwanthlm/EKS-Terraform-Jenkins.git
cd EKS-Terraform-Jenkins
```

### 2. Run the Installer Script

The installer script will install Jenkins, Terraform, Kubernetes (kubectl), and AWS CLI on your server.

```bash
chmod +x installer.sh
./installer.sh
```

### 3. Configure Jenkins

Ensure that Jenkins has the following environment variables configured:

- **`AWS_ACCESS_KEY_ID`**
- **`AWS_SECRET_ACCESS_KEY`**
- **`AWS_DEFAULT_REGION`** (Set to `us-east-1`)

### 4. Set Up the Terraform Infrastructure

Inside the `terraform` directory, initialize and apply the Terraform scripts:

```bash
cd terraform
terraform init
terraform validate
terraform plan
terraform apply --auto-approve
```

This will set up the AWS VPC, EKS cluster, and associated resources.

### 5. Deploy the NGINX Application

Navigate to the `manifests` directory and apply the Kubernetes manifests:

```bash
cd ../manifests
kubectl apply -f deployment.yml
kubectl apply -f service.yml
```

### 6. Access the NGINX Application

Once the LoadBalancer is created, you can retrieve the external IP using:

```bash
kubectl get svc nginx-service
```

Visit the external IP in your web browser to see the running NGINX application.

## Jenkins Pipeline

The `Jenkinsfile` defines the following stages in the CI/CD pipeline:

1. **Checkout SCM**: Pulls the latest code from the Git repository.
2. **Initializing Terraform**: Initializes Terraform in the `terraform` directory.
3. **Validating Terraform**: Validates the Terraform configuration.
4. **Previewing the Infrastructure**: Previews the infrastructure changes.
5. **Create/Destroy an EKS Cluster**: Applies or destroys the Terraform configuration.

### Example Pipeline Execution

You can trigger the Jenkins pipeline manually or set it up to run automatically on every push to the `main` branch.

## Known Issues

- **Permission Denied**: Ensure that Jenkins or the user running the Terraform scripts has the necessary permissions on the `/opt/nomad` directory.

## License
-

## Contact

For any questions or issues, please reach out to Aniket (aniket2026.purohit@mue.edu.in).

---

Feel free to customize this README file further as per your needs!
