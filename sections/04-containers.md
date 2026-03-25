# **Containers on AWS: ECS, EKS, Fargate**

Containers abstract the runtime environment. The exam asks which container platform fits the scenario.

| Service | Description | Launch Types | When to Choose |
| ----- | ----- | ----- | ----- |
| ECS (Elastic Container Service) | AWS-native container orchestration; simpler, tightly integrated | EC2 (you manage servers) or Fargate (serverless) | "AWS-native", "simpler Kubernetes alternative", "Docker on AWS" |
| EKS (Elastic Kubernetes Service) | Managed Kubernetes; industry standard; portable | EC2, Fargate, or AWS Outposts | "Kubernetes", "multi-cloud", "team knows K8s", "complex orchestration" |
| Fargate | Serverless compute engine for containers (ECS or EKS) | N/A — it IS the launch type | "no server management", "don't want to patch EC2" |
| App Runner | Fully managed; source code or container → auto-scaled web service | Fully managed (no choice) | "simplest deployment", "just run my web app", "developer-focused" |
| ECR (Elastic Container Registry) | Managed Docker container registry | N/A — storage only | Store Docker images privately on AWS; integrates natively with ECS/EKS |

| ⚠️ EXAM TRAP: Fargate is NOT a service you choose independently — it's a launch type for ECS or EKS. When a question says 'serverless containers,' they want ECS/EKS with Fargate launch type, NOT a separate Fargate service. |
| :---- |

| SECTION 3 — STORAGE: S3, EBS, EFS, GLACIER & MORE |
| :---: |

---

[< AWS Lambda](03-lambda.md) | [Back to README](../README.md) | [S3 - Simple Storage Service >](05-s3.md)
