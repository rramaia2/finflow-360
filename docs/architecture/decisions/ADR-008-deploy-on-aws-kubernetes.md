# ADR-008: Deploy on AWS Using Kubernetes

## Status

Accepted

## Context

FinFlow 360 contains multiple independently deployable services, Kafka consumers, frontend applications, and supporting infrastructure.

The platform must support containerized deployment, service discovery, horizontal scaling, rolling updates, health checks, secrets management, monitoring, and automated recovery.

## Decision

Deploy FinFlow 360 on AWS using Docker containers and Amazon Elastic Kubernetes Service.

Use Terraform to provision AWS infrastructure and Kubernetes resources. Use Amazon RDS for PostgreSQL and Amazon MSK or a compatible managed Kafka service for event streaming.

## Alternatives considered

- Deploy directly to Amazon EC2

- Use AWS Elastic Beanstalk

- Use Amazon ECS with Fargate

- Use AWS Lambda for all backend processing

- Deploy to a self-managed Kubernetes cluster

## Benefits

- Independent deployment and scaling of services

- Standard container orchestration

- Rolling deployments and automated recovery

- Health checks and resource management

- Portability between Kubernetes and OpenShift environments

- Infrastructure automation through Terraform

- Integration with AWS networking, IAM, monitoring, and secret management

## Tradeoffs

- Kubernetes introduces operational complexity

- EKS and managed supporting services increase cost

- Cluster security and networking require specialized knowledge

- Incorrect resource requests or limits can affect reliability

- Deployment pipelines require environment-specific configuration

## Consequences

Every service must provide readiness and liveness endpoints and define CPU and memory requests and limits.

Kubernetes manifests or Helm charts must be version-controlled. Secrets must be stored using AWS Secrets Manager or another approved secrets solution rather than committed to Git.

Terraform will provision networking, IAM, EKS, RDS, Kafka, container registries, and monitoring resources.

CI/CD pipelines must build and scan Docker images, deploy them to development and staging environments, run smoke tests, and support controlled rollback.