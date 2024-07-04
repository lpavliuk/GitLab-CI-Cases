# GitLab CI Cases

The complex and interesting GitLab CIs cases that I had to build in my career.

---
### CI: [cdk-ecr-ecs-cluster.gitlab-ci.yml](cdk-ecr-ecs-cluster.gitlab-ci.yml)

**Case:** A repository consists of a backend API application source code including CDK code to provision the application's resources
on AWS. The application has a Dockerfile and is hosted in the AWS ECS Cluster.

Environments:
- `dev` (Development)
- `qa` (QA)
- `prod` (Production)

The CI must do the following things:
- Build Docker Image and upload it to AWS ECR;
- Run CDK code to provision the application's resources on AWS using IAM Role;
- Trigger ECS Task Definition to launch new containers with the updated image;

AWS Services are used in the CI:
- **IAM Identity Provider** - assuming CI IAM Role via [GitLab OpenID Connect](https://docs.gitlab.com/ee/ci/cloud_services/aws/);
- **AWS CDK** - provisioning;
- **AWS ECR** - docker image registry;
- **AWS ECS** - task definition update;

CI Environment Variables:
- `CDK_ENV_FILE` (type: `file`) - CDK .env file contents

---
### CI: [cdk-cloudfront-s3.gitlab-ci.yml](cdk-cloudfront-s3.gitlab-ci.yml)

**Case:** A repository consists of a frontend application source code including CDK code to provision the application's resources
on AWS. The application is hosted on AWS CloudFront + S3 Bucket as an origin.

Environments:
- `dev` (Development)
- `qa` (QA)
- `prod` (Production)

The CI must do the following things:
- Run CDK code to provision the application's resources on AWS using IAM Role;
- Install dependencies and build an application;
- Upload the built to S3 Bucket;
- Create CloudFront cache invalidation;

AWS Services are used in the CI:
- **IAM Identity Provider** - assuming CI IAM Role via [GitLab OpenID Connect](https://docs.gitlab.com/ee/ci/cloud_services/aws/);
- **AWS CDK** - provisioning;
- **AWS CloudFront** - distribution;
- **AWS S3 Bucket** - storage for static files; 

CI Environment Variables:
- `CDK_ENV_FILE` (type: `file`) - CDK .env file contents
