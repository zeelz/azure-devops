# Express TypeScript CI/CD with Azure DevOps

A simple CI/CD pipeline that automates building, testing, and deploying a TypeScript Express application from GitHub to an AWS EC2 instance.

## Pipeline currently disabled

## Architecture

```text
GitHub (main branch)
       |
       v
 Azure DevOps Pipeline
       |
       v
   BUILD (CI)
   - Install dependencies
   - Run tests
   - Compile TypeScript
   - Publish artifact
       |
       v
  DEPLOY (CD)
   - Download artifact
   - Transfer files via SSH
   - Install production dependencies
   - Restart application with PM2
       |
       v
 AWS EC2 (Ubuntu 24.04)
```

## Tech Stack

- **Application:** Node.js, Express.js, TypeScript
- **Source Control:** GitHub
- **CI/CD:** Azure DevOps Pipelines (YAML)
- **Hosting:** AWS EC2 (Ubuntu 24.04)
- **Deployment:** SSH
- **Process Management:** PM2

## Setup

**EC2 prerequisites:**
- Node.js 22 and npm
- PM2 installed globally
- SSH access configured
- Application directory: `/home/ubuntu/apps/express-app`

## Create an SSH service connection in Azure DevOps
This is how Azure DevOps will securely connect to your EC2 instance.
1. Log in to Azure DevOps.
2. Open your project.
3. Navigate to Project Settings → Service connections.
4. Select New service connection.
5. Choose SSH.

**Azure DevOps:**

1. Connect your GitHub repository.
2. Create an SSH service connection named `aws-ec2-ssh`.
3. Add `azure-pipelines.yml` to your repository.
4. Configure the pipeline to use the YAML file.

## Deployment

Push changes to the `main` branch to trigger the pipeline:

```bash
git add .
git commit -m "feat: update application"
git push origin main
```

Azure DevOps automatically builds, tests, packages, and deploys the application to EC2.

## Future Improvements

- Secure environment variables and secrets management
- Staging and production environments
- Deployment approvals
- Automated health checks and rollback
- Docker-based deployments

