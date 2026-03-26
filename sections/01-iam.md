# **IAM — Identity & Access Management**

**What it is:** IAM is the global service that controls WHO can do WHAT to WHICH AWS resources. It is free, global (not region-specific), and foundational to every AWS architecture.

## **Core IAM Components**

| Component | What it is | Real-World Analogy | Key Exam Fact |
| ----- | ----- | ----- | ----- |
| User | A permanent identity for a person or application | An employee badge | Has long-term credentials (password \+ access keys) |
| Group | A collection of users sharing the same permissions | A department (HR, Dev, Finance) | Groups cannot be nested; policies attach to groups, not directly to users best practice |
| Role | A temporary identity assumed by services, users, or external accounts | A visitor badge you wear and return | No long-term credentials; uses STS tokens (15 min–36 hrs) |
| Policy | JSON document defining Allow/Deny for actions on resources | A rulebook/terms of service | Explicit Deny always wins over any Allow |
| STS | Security Token Service — issues temporary credentials | A temp-pass vending machine | AssumeRole, AssumeRoleWithWebIdentity, GetFederationToken |

## **IAM Policy Evaluation Logic**

AWS evaluates policies in a strict priority order. Knowing this order is critical for the exam.

| Priority | Evaluation Step | Result |
| ----- | ----- | ----- |
| 1 (highest) | Explicit Deny in ANY policy | DENY — game over, no exceptions |
| 2 | Organizations SCP (Service Control Policy) | If SCP doesn't Allow → DENY |
| 3 | Resource-based policy (e.g. S3 bucket policy) | May grant cross-account access |
| 4 | Identity-based policy (IAM policy on user/role) | Explicit Allow needed |
| 5 | Permission Boundary | Must also Allow what identity policy allows |
| 6 (lowest) | Session Policy (when assuming roles) | Further restricts temporary session |

| ⚠️ EXAM TRAP: No explicit Allow \= implicit DENY. A user with no policies attached cannot do anything at all. This trips up many candidates who assume a blank slate allows read-only access. |
| :---- |

## **IAM Roles — The Most Important IAM Concept for SAA**

Roles are used constantly in SAA exam scenarios. Learn to recognize WHEN to use a role vs other options.

| Scenario | Solution | Why Not Alternatives |
| ----- | ----- | ----- |
| EC2 instance needs to read S3 | Attach IAM Role to EC2 instance profile | Never store access keys on EC2 — they can be stolen from metadata |
| Lambda needs to write to DynamoDB | Execution Role on Lambda function | Same reasoning — roles provide temp creds automatically |
| Account A needs to access Account B's S3 | Role in Account B; Account A users AssumeRole | Cross-account access \= Roles, not copying credentials |
| Mobile app users (millions) need AWS access | Cognito Identity Pool \+ Web Identity Federation | Cannot create IAM user per customer — doesn't scale |
| On-prem employees need AWS access via AD | AWS SSO / IAM Identity Center with AD connector | Federation with SAML 2.0 — no AWS user creation needed |
| Third-party audit needs read-only access | Role with External ID (Confused Deputy protection) | External ID prevents one tenant impersonating another |

## **IAM Policies: Inline vs Managed**

| Type | Description | When to Use | Exam Tip |
| ----- | ----- | ----- | ----- |
| AWS Managed Policy | Pre-built by AWS (e.g. AmazonS3ReadOnlyAccess) | Starting point, common use cases | Cannot modify; may be overly permissive |
| Customer Managed Policy | You create and maintain; reusable across entities | Production environments, least privilege | Version-controlled; best practice for shared policies |
| Inline Policy | Embedded directly in one user/role/group; deleted with entity | Strict 1:1 relationship needed | Hard to audit; generally discouraged |

## **Permission Boundaries**

**What it does:** Sets the MAXIMUM permissions an IAM entity can have. The effective permissions are the intersection of the identity policy and the permission boundary.

**Use case:** You want to allow developers to create IAM roles/users for their services, but ensure they cannot grant more permissions than they themselves have (prevents privilege escalation).

| 💡 TIP: Think of Permission Boundary as a fence. The identity policy says what they CAN do. The boundary says what the fence allows. Only actions inside BOTH the fence AND the policy are permitted. |
| :---- |

## **MFA & Security Best Practices**

| Practice | Details |
| ----- | ----- |
| Root Account | Enable MFA immediately; never use for day-to-day tasks; delete access keys |
| MFA Delete on S3 | Requires MFA to delete S3 objects or change bucket versioning — needs root account to enable |
| Access Key Rotation | Rotate every 90 days; use IAM Access Analyzer to find unused keys |
| Least Privilege | Start with minimal permissions and add as needed; use Access Advisor to see what's used |
| IAM Access Analyzer | Identifies resources shared outside your org/account (unintended public exposure) |

| 🧠 MNEMONIC: GRUELS for IAM entities: Groups, Roles, Users, External IDs, Limits (boundaries), STS. Everything in IAM connects to these six. |
| :---- |

| NEXT: SECTION 2 — COMPUTE: EC2, LAMBDA, CONTAINERS & MORE |
| :---: |

---

[Back to README](../README.md) | [EC2 - Elastic Compute Cloud >](02-ec2.md)
