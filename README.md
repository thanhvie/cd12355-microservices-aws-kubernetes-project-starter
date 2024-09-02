# Coworking Analytics Application Deployment

## Overview

This repository contains the Coworking Analytics application, which is deployed on an Amazon EKS cluster. The application is a Flask-based service with PostgreSQL as its database. It is containerized using Docker and monitored using Amazon CloudWatch.

## Technologies and Tools

- **Amazon EKS**: Managed Kubernetes service for deploying and managing the application.
- **Amazon ECR**: Docker container registry for storing and versioning Docker images.
- **Docker**: Used to containerize the application for consistent deployment across environments.
- **Kubernetes**: Manages containerized applications across a cluster of machines.
- **Amazon CloudWatch**: Monitors and logs application performance and infrastructure metrics.

## Deployment Process

1. **Docker Image Creation**: The application is packaged as a Docker image, which is stored in Amazon ECR. The Dockerfile is located in the `analytics/` directory.
2. **Continuous Integration**: CodeBuild is set up to trigger on GitHub commits, automatically building and pushing the Docker image to ECR. The buildspec.yml file defines the build process.

3. **Kubernetes Deployment**: The `coworking.yaml` file in the `deployment/` directory defines the Kubernetes deployment. It pulls the Docker image from ECR and deploys it to the EKS cluster.

4. **Database Configuration**: PostgreSQL configuration is managed via Kubernetes ConfigMaps and Secrets, ensuring secure and consistent database connections.

5. **Monitoring**: CloudWatch Container Insights is enabled via the CloudWatch Observability EKS add-on, providing infrastructure metrics and application logs under `/aws/containerinsights/my-cluster/application`.

## Releasing New Builds

1. **Code Changes**: Commit changes to the repository. CodeBuild automatically triggers a new build and pushes the updated Docker image to ECR.

2. **Deploying Updates**: Run `kubectl apply -f deployment/coworking.yaml` to update the Kubernetes deployment with the latest Docker image.

3. **Monitoring**: Use CloudWatch to monitor logs and metrics for the application. Ensure that the application is performing as expected by checking health and readiness probes.

## Scaling and Rollbacks

- **Scaling**: Adjust the `replicas` field in the deployment YAML to scale the application.
- **Rollbacks**: Use `kubectl rollout undo deployment/coworking` to revert to a previous deployment if necessary.

## Conclusion

This setup ensures that the Coworking Analytics application is robustly deployed on Amazon EKS with continuous integration and monitoring in place. For any further customization or troubleshooting, refer to the AWS and Kubernetes documentation.
