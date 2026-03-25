# ☁️ AWS Certified Solutions Architect – Associate (SAA-C03) | Master Cheatsheet & Exam Guide

[![AWS](https://img.shields.io/badge/AWS-SAA--C03-orange?style=flat&logo=amazonaws)](https://aws.amazon.com/certification/certified-solutions-architect-associate/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Sections](https://img.shields.io/badge/Sections-26-green)]()

> **By Devesh Talreja**

---

## 📖 About These Notes

I've created these notes during my **AWS Certified Solutions Architect – Associate (SAA-C03)** exam preparation and used them heavily during revision — going through each section multiple times to reinforce concepts, memorize key differences, and drill exam traps. These notes were built alongside my learning and practice tests, with AI helping me articulate and consolidate concepts as I studied.

What makes these notes useful:
- **Exam-focused:** Every table, comparison, and callout is written with the exam in mind — not theory, but what you actually need to answer questions correctly
- **High-signal, low-noise:** Covers the right depth — enough to understand, not so much you get lost
- **Comparison-heavy:** The trickiest exam questions test your ability to distinguish similar services — this guide is built around those distinctions
- **Battle-tested:** These are the exact notes I revised with before passing the exam

I'm happy to help fellow AWS learners — feel free to use these as your revision companion, share them, or open an issue if you spot anything outdated.

---

## 📚 Table of Contents

| #  | Section                                                                           | What's Inside                                                                                                 |
| -- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| 1  | [IAM — Identity &amp; Access Management](sections/01-iam.md)                        | Users, Groups, Roles, Policies, STS, Permission Boundaries, MFA best practices                                |
| 2  | [EC2 — Elastic Compute Cloud](sections/02-ec2.md)                                   | Instance families, Purchasing options (On-Demand/Reserved/Spot/Dedicated), ASG, Placement Groups, EBS/EFS/FSx |
| 3  | [AWS Lambda](sections/03-lambda.md)                                                  | Execution limits, Concurrency (reserved/provisioned), Triggers, Destinations, Error Handling                  |
| 4  | [Containers on AWS: ECS, EKS, Fargate](sections/04-containers.md)                    | ECS vs EKS vs Fargate vs App Runner, ECR, when to use each                                                    |
| 5  | [S3 — Simple Storage Service](sections/05-s3.md)                                    | Storage classes, Lifecycle policies, Security layers, Encryption types, CRR/SRR, Performance                  |
| 6  | [Storage Gateway](sections/06-storage-gateway.md)                                    | S3 File Gateway, FSx File Gateway, Volume Gateway (Cached/Stored), Tape Gateway                               |
| 7  | [Database Selection Guide](sections/07-database-selection.md)                        | RDS vs Aurora vs DynamoDB vs Redshift vs Neptune — full decision table                                       |
| 8  | [RDS — Relational Database Service](sections/08-rds.md)                             | Multi-AZ vs Read Replicas (classic confusion), Backups, PITR                                                  |
| 9  | [Aurora — The Exam Favorite](sections/09-aurora.md)                                 | Cluster storage architecture, Serverless v2, Backtrack, Global Database                                       |
| 10 | [DynamoDB — The Serverless NoSQL Giant](sections/10-dynamodb.md)                    | Partition/Sort keys, LSI vs GSI, DAX, Streams, Global Tables, Transactions, TTL                               |
| 11 | [ElastiCache — Caching Strategies](sections/11-elasticache.md)                      | Redis vs Memcached, Lazy Loading, Write-Through, Write-Behind, TTL                                            |
| 12 | [VPC — Virtual Private Cloud](sections/12-vpc.md)                                   | Subnets, IGW, NAT Gateway, SG vs NACL, Peering, Transit Gateway, PrivateLink, Flow Logs                       |
| 13 | [Route 53 — DNS &amp; Routing Policies](sections/13-route53.md)                     | All 8 routing policies, Health Checks, Geolocation vs Geoproximity                                            |
| 14 | [CloudFront — Content Delivery Network](sections/14-cloudfront.md)                  | Origins, OAC, Signed URLs/Cookies, Lambda@Edge vs CF Functions, WAF, Field Encryption                         |
| 15 | [Elastic Load Balancing — Three Types Compared](sections/15-load-balancing.md)      | ALB vs NLB vs GWLB, Advanced ALB routing, Connection Draining                                                 |
| 16 | [Messaging &amp; Event-Driven Architecture](sections/16-messaging.md)                | SQS (Standard/FIFO), SNS, EventBridge, Kinesis Streams/Firehose/Analytics, MSK, MQ                            |
| 17 | [Monitoring Stack — CloudWatch, CloudTrail, Config](sections/17-monitoring.md)      | Metrics, Logs, Alarms, CloudTrail audit, AWS Config compliance, X-Ray tracing                                 |
| 18 | [Security Services — Know Your Defense Layers](sections/18-security.md)             | WAF, Shield, GuardDuty, Inspector, Macie, KMS, CloudHSM, Secrets Manager, Firewall Manager                    |
| 19 | [Core Architectural Patterns for SAA](sections/19-architectural-patterns.md)         | HA Web App, Serverless Pattern, DR strategies (RTO/RPO), Data Lake, Event-Driven, Well-Architected 6 Pillars  |
| 20 | [Migration Services](sections/20-migration.md)                                       | DMS + SCT, Application Migration Service, Snowball/Snowmobile, DataSync, Transfer Family                      |
| 21 | [Analytics Services](sections/21-analytics.md)                                       | Athena, Redshift, EMR, Glue, QuickSight, OpenSearch, Lake Formation                                           |
| 22 | [Application Integration &amp; Orchestration](sections/22-app-integration.md)        | Step Functions, AppFlow, API Gateway (REST vs HTTP), AppSync, SWF                                             |
| 23 | [Other Important Services](sections/23-other-services.md)                            | CloudFormation, CDK, Elastic Beanstalk, SSM, Organizations, Control Tower, Global Accelerator, Outposts       |
| 24 | [Most-Confused Services &amp; Concepts](sections/24-common-confusions.md)            | Side-by-side: GA vs CloudFront, SQS vs SNS vs Kinesis, EBS vs EFS vs S3, Multi-AZ variations, Cognito Pools   |
| 25 | [Exam-Style Practice Questions](sections/25-practice-questions.md)                   | 10 scenario-based questions across all 4 SAA domains with full explanations                                   |
| 26 | [Summary: Service Selection by Problem Type](sections/26-summary-quick-reference.md) | "I need to store/compute/connect/secure..." quick-pick tables + Key numbers to memorize + Final tips          |

---

## 🚀 How to Use These Notes

### Recommended Study Path

This is how I approached my prep — adapt it to what works for you:

1. **Take a video course first** — I went through Stephane Maarek's AWS SAA course on Udemy (highly recommended). After each section in the course, come back and read the corresponding notes here to reinforce what you just learned.
2. **Do hands-on practice** — Reading isn't enough. Make sure to get hands-on experience in the AWS console by building small test projects or doing labs to cement the concepts in your mind.
3. **Use these notes for revision** — Once you've completed the course, go through all 26 sections here as your revision guide. Pay extra attention to sections 24 (Common Confusions) and 26 (Quick Reference) — they are highest-yield for the exam.
4. **Do practice exams** — This is non-negotiable. Tutorial Dojo's SAA practice tests and Stephane Maarek's practice exams are both excellent and very close to the real exam style. Score consistently above 80% before booking.
5. **Day before the exam** — Only review section 26 (Quick Reference): key numbers, service selection summaries, and final exam-day tips.

### Reading the Callouts

Each section uses consistent callout formatting:

- **⚠️ EXAM TRAP** — The most commonly missed concepts; these directly address wrong answer choices
- **💡 TIP** — Practical exam strategy and "when to use what" guidance
- **🧠 MNEMONIC** — Memory aids for complex comparisons (e.g., "C = CPU crunching" for Compute Optimized)
- **📌 NOTE** — Additional context before answers in practice questions

### Navigation

Every section file has **← prev | README | next →** links at the bottom so you can move through sections without coming back to this page.

Feel free to **fork** or **⭐ star** this repo to keep it bookmarked so you can easily come back for your revision rounds!

---

## ⚠️ Disclaimer

These are personal study notes, not official AWS documentation. AWS services evolve constantly — always verify with the [official AWS docs](https://docs.aws.amazon.com/) for the latest details. Content is intentionally simplified in places to aid memorization and is optimized for exam preparation, not production architecture decisions.

---

## 🔗 Official AWS Resources

| Resource | Link |
|----------|------|
| SAA-C03 Exam Guide | [Certified Solutions Architect – Associate](https://aws.amazon.com/certification/certified-solutions-architect-associate/) |
| SAA-C03 Exam Guide PDF | [Download Exam Guide](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Exam-Guide.pdf) |
| AWS Official Documentation | [docs.aws.amazon.com](https://docs.aws.amazon.com/) |
| AWS Well-Architected Framework | [Well-Architected](https://aws.amazon.com/architecture/well-architected/) |
| AWS Architecture Center | [Architecture Center](https://aws.amazon.com/architecture/) |
| AWS Whitepapers | [aws.amazon.com/whitepapers](https://aws.amazon.com/whitepapers/) |
| AWS FAQs | [aws.amazon.com/faqs](https://aws.amazon.com/faqs/) |
| AWS Skill Builder (free labs) | [skillbuilder.aws](https://skillbuilder.aws/) |
| AWS Free Tier | [aws.amazon.com/free](https://aws.amazon.com/free/) |
| Stephane Maarek – SAA Course | [Udemy Course](https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/) |
| Stephane Maarek – Practice Exams | [Udemy Practice Tests](https://www.udemy.com/course/practice-exams-aws-certified-solutions-architect-associate/) |
| Tutorial Dojo – Practice Exams | [tutorialsdojo.com](https://tutorialsdojo.com/courses/aws-certified-solutions-architect-associate-practice-exams/) |
| AWS re:Post (community Q&A) | [repost.aws](https://repost.aws/) |

---

## 🤝 Contributing

We welcome contributions from the community to keep this cheat sheet up-to-date! If you have suggestions, corrections, or additional content to add, please:

1. [Fork the repository](https://github.com/devesh-talreja/aws-saa-cheatsheet/fork)
2. Create a feature branch
3. Submit a pull request with your changes

## 📄 License

This cheat sheet is released under the MIT License. Feel free to use, modify, and share it as needed.

---

**Happy Learning and Best of Luck with Your AWS-SAA Certification! 🎉 Gambare! ☁️**
*— Devesh Talreja*
