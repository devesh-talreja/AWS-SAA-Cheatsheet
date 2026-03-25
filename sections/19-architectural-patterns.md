# **Core Architectural Patterns for SAA**

## **1\. Highly Available Web Application (The Classic Pattern)**

This pattern appears in some form in nearly every SAA exam. Know it cold.

| Layer | Service(s) | Why |
| ----- | ----- | ----- |
| DNS | Route 53 (Latency or Failover policy) | Global DNS with health checks; route users to nearest/healthy region |
| CDN | CloudFront | Cache static assets; reduce origin load; SSL termination at edge |
| Load Balancer | ALB (Multi-AZ) | Distribute traffic across AZs; path-based routing; health checks |
| Web Tier | EC2 in ASG across 2+ AZs (or ECS/Fargate) | Horizontal scaling; AZ fault tolerance |
| App Tier | EC2/Lambda in private subnets across 2+ AZs | Isolation from web tier; auto-scaling |
| Cache | ElastiCache (Redis) — replicated across AZs | Reduce DB read load; session storage |
| Database | Aurora Multi-AZ or RDS Multi-AZ \+ Read Replicas | HA for writes (Multi-AZ) \+ scale reads (replicas) |
| Storage | S3 for static assets and uploads | Durable, scalable object storage outside EC2 |
| Secrets | Secrets Manager or Parameter Store | No hardcoded credentials anywhere |
| Network | VPC with public/private subnets; NAT Gateway per AZ | Security isolation; outbound internet for private tier |

## **2\. Serverless Architecture Pattern**

| Layer | Service | Notes |
| ----- | ----- | ----- |
| API Layer | API Gateway (REST or HTTP API) | HTTP API \= cheaper, lower latency. REST API \= more features (usage plans, API keys, WAF). |
| Compute | Lambda | Functions triggered by API GW; 15 min max; stateless |
| Database | DynamoDB (serverless) | On-Demand capacity; single-digit ms; no server management |
| Cache | DAX (for DynamoDB) or ElastiCache | DAX \= transparent, microsecond reads. ElastiCache \= more control, broader use. |
| Auth | Cognito User Pools \+ Identity Pools | User Pool \= auth/login. Identity Pool \= exchange token for AWS credentials. |
| Storage | S3 | Store files; trigger Lambda on upload |
| Events | EventBridge or SNS \+ SQS | Async workflows between Lambda functions |
| CDN | CloudFront | Serve SPA (React/Vue) from S3 \+ API calls via CloudFront |

| 💡 TIP: REST API vs HTTP API in API Gateway: HTTP API costs 71% less and has lower latency. REST API adds: usage plans, API keys, request transformation, AWS WAF, resource policies, edge-optimized. For exam: need usage plans/throttling per client or WAF → REST API. Otherwise → HTTP API. |
| :---- |

## **3\. Disaster Recovery Patterns — RTO/RPO Decision**

| Strategy | RTO | RPO | Cost | How it Works |
| ----- | ----- | ----- | ----- | ----- |
| Backup & Restore | Hours | Hours | Lowest | Backups to S3 or Glacier; restore from scratch. No standby environment. |
| Pilot Light | 10s of minutes | Minutes | Low | Minimal core services always running (DB replication ON); scale up app tier during DR. |
| Warm Standby | Minutes | Seconds to minutes | Medium | Scaled-down full environment running; scale to production size during DR. |
| Multi-Site Active/Active | Near zero | Near zero | Highest | Full production in 2+ regions simultaneously; Route 53 routes to both. |

| 🧠 MNEMONIC: BR-PP-WS-AA: Backup-Restore (hours), Pilot-light (minutes), Warm-Standby (minutes, more ready), Active-Active (near zero). Cost goes UP as RTO/RPO goes DOWN. |
| :---- |

## **4\. Data Lake Architecture Pattern**

| Layer | Services | Purpose |
| ----- | ----- | ----- |
| Ingestion | Kinesis Data Streams / Firehose, AWS DMS, AWS DataSync, Snowball Edge | Collect data from apps, databases, on-prem |
| Storage (Raw) | S3 (with partitioning by date/source) | Raw landing zone; immutable source of truth |
| Catalog | AWS Glue Data Catalog | Metadata store; tables schemas; partitions |
| ETL/Transform | AWS Glue (Spark jobs), Lambda | Clean, transform, enrich data |
| Storage (Curated) | S3 (Parquet/ORC format) | Transformed data ready for analysis |
| Query | Amazon Athena (SQL on S3) | Serverless; pay per query; no DB provisioning |
| Visualization | QuickSight | BI dashboards; ML-powered insights |
| Warehouse | Redshift (for complex OLAP) | For heavy analytics workloads; Redshift Spectrum queries S3 directly |

## **5\. Event-Driven Decoupled Architecture**

**Pattern:** Producers emit events → Event bus (EventBridge/SNS) → Multiple consumers process independently. Components are loosely coupled; changes to one don't affect others.

| Scenario | Pattern | Services |
| ----- | ----- | ----- |
| Order placed → notify inventory, billing, and shipping simultaneously | Fan-out | SNS → 3 SQS queues (one per service) |
| Batch processing with retry on failure | Queue \+ Worker | SQS (Standard) → ASG of workers → DLQ for failures |
| React to CloudTrail API events (e.g., non-compliant resource created) | Event rule | EventBridge rule matching event pattern → Lambda remediation |
| Process uploaded files asynchronously | S3 Event \+ Queue | S3 PUT → S3 Event Notification → SQS → Lambda/ECS worker |
| Microservice workflow with compensation | Step Functions | Step Functions state machine orchestrating Lambda steps with error handling |

## **6\. Well-Architected Framework — 6 Pillars**

| Pillar | Core Question | Key AWS Tools |
| ----- | ----- | ----- |
| Operational Excellence | How do you run and monitor systems to deliver business value? | CloudFormation (IaC), CloudWatch, AWS Config, X-Ray, Systems Manager |
| Security | How do you protect information and systems? | IAM, KMS, CloudTrail, GuardDuty, Shield, WAF, Macie, Security Hub |
| Reliability | How do you recover from failures and meet demand? | Route 53, Auto Scaling, Multi-AZ/Multi-Region, Backups, Circuit Breakers |
| Performance Efficiency | How do you use resources efficiently? | Auto Scaling, Lambda, ElastiCache, CloudFront, Graviton instances |
| Cost Optimization | How do you avoid unnecessary costs? | Reserved/Spot Instances, S3 Intelligent-Tiering, Trusted Advisor, Cost Explorer, Savings Plans |
| Sustainability | How do you minimize environmental impact? | Graviton (better performance/watt), serverless, right-sizing, Managed Services |

| SECTION 10 — ADDITIONAL SERVICES: MIGRATION, ANALYTICS, ML & MORE |
| :---: |

---

[< Security Services - Know Your Defense Layers](18-security.md) | [Back to README](../README.md) | [Migration Services >](20-migration.md)
