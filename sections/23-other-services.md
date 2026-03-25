# **Other Important Services**

| Service | Purpose | SAA Exam Angle |
| ----- | ----- | ----- |
| CloudFormation | Infrastructure as Code (IaC) — JSON/YAML templates | Reproducible infrastructure; drift detection; nested stacks for complex architectures; StackSets for multi-account/region |
| CDK (Cloud Development Kit) | IaC using programming languages (TypeScript, Python, Java) | Compiles to CloudFormation; developer-friendly |
| Elastic Beanstalk | PaaS: deploy code, AWS manages infra | Developers upload code → EB handles EC2, ASG, ELB, RDS; not for complex architectures |
| OpsWorks | Managed Chef/Puppet configuration management | Legacy; used when existing Chef/Puppet tooling must be preserved |
| Systems Manager (SSM) | Operational management of EC2/on-prem instances | Run Command (execute scripts without SSH); Patch Manager; Session Manager (browser SSH no port 22); Parameter Store |
| AWS Organizations | Centrally manage multiple AWS accounts | Service Control Policies (SCPs) restrict what member accounts can do; consolidated billing; OU hierarchy |
| AWS Control Tower | Set up multi-account landing zone with guardrails | Uses Organizations \+ SSO \+ Config \+ CloudTrail; account vending machine via Account Factory |
| AWS Trusted Advisor | Best practice checks across 5 categories | Cost optimization, performance, security, fault tolerance, service limits; Business/Enterprise support for all checks |
| AWS Cost Explorer | Visualize and analyze AWS costs | Forecasts, reserved instance recommendations, savings plans recommendations |
| AWS Budgets | Set spending alerts and take action | Alert when cost \> threshold; trigger SNS or take action; budget for cost/usage/RI coverage |
| Cognito | User authentication and authorization for apps | User Pools \= user directory \+ auth (login). Identity Pools \= exchange tokens for AWS temp credentials. Often used together. |
| AWS Global Accelerator | Improve global app performance using AWS network | Static anycast IPs; routes to nearest healthy endpoint via AWS backbone; good for TCP/UDP non-HTTP traffic; vs CloudFront (HTTP/cache) |
| AWS Outposts | AWS hardware in your data center | Same AWS APIs/tools on-premises; for low-latency local data processing or data residency requirements |
| AWS Wavelength | AWS infrastructure embedded in telecom 5G networks | Ultra-low latency to mobile/connected devices; no traffic leaves telecom provider network |
| AWS Local Zones | AWS infrastructure in metro areas outside main regions | Single-digit ms latency to specific cities; extension of a parent region |

| SECTION 11 — THE 'WHICH ONE?' QUICK REFERENCE (COMMON CONFUSIONS) |
| :---: |

---

[< Application Integration and Orchestration](22-app-integration.md) | [Back to README](../README.md) | [Most-Confused Services and Concepts >](24-common-confusions.md)
