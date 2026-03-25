# **Most-Confused Services & Concepts**

## **Global Accelerator vs CloudFront**

| Dimension | Global Accelerator | CloudFront |
| ----- | ----- | ----- |
| What it does | Routes TCP/UDP traffic globally via AWS backbone to nearest healthy endpoint | CDN that caches HTTP/HTTPS content at edge locations |
| Caching? | NO — purely routing/load balancing | YES — main feature; caches static and dynamic content |
| Protocol | Any TCP/UDP (HTTP included but not specialized) | HTTP/HTTPS/WebSocket only |
| IP Addresses | 2 static anycast IPs globally (good for whitelisting) | Dynamic — IPs change; use domain only |
| Best for | Gaming (UDP), IoT, VoIP, APIs without caching, failover for non-HTTP | Web apps, media delivery, static/dynamic web content |
| Health checks | Yes — routes away from unhealthy endpoints instantly | Via origin health checks \+ custom error responses |
| Exam keyword | "static IP", "non-HTTP", "gaming", "failover globally", "consistent performance" | "cache", "CDN", "reduce origin load", "static assets", "media streaming" |

## **SQS vs SNS vs Kinesis**

| Dimension | SQS | SNS | Kinesis |
| ----- | ----- | ----- | ----- |
| Pattern | Queue (pull) | Pub/Sub (push) | Stream (pull) |
| Ordering | Standard: best effort; FIFO: guaranteed | No ordering | Ordered within shard |
| Persistence | 14 days | None (push only) | 1-365 days |
| Consumers | One consumer (competing), FIFO \= one at a time | Multiple (up to 12.5M) | Multiple (unlimited with enhanced fan-out) |
| Throughput | Nearly unlimited (Standard) | Nearly unlimited | Provisioned (shards); On-Demand mode available |
| Replay | No | No | Yes |
| Use case | Worker pools, decoupling, buffering | Notifications, fan-out | Real-time analytics, click stream, IoT |

## 

## 

## **EBS vs EFS vs S3**

| Dimension | EBS | EFS | S3 |
| ----- | ----- | ----- | ----- |
| Type | Block storage | File storage (NFS) | Object storage |
| Attach to | Single EC2 (same AZ); io1/io2 Multi-Attach (same AZ) | Many EC2 instances across AZs (Linux) | Accessed via HTTP/HTTPS (not mountable natively) |
| Scope | Single AZ | Multi-AZ regional | Global (regional bucket, globally accessible) |
| Scaling | Manual (increase volume size) | Auto-scales | Unlimited auto-scales |
| Performance | Up to 256,000 IOPS (io2) | Throughput scales with size; Provisioned Throughput mode | High throughput; best for large objects |
| Use case | OS boot volumes, databases | Shared config files, CMS content, web serving | Backup, archives, static websites, data lake |
| Cost model | Per GB provisioned | Per GB stored (+ throughput mode option) | Per GB stored \+ requests \+ data transfer |

## **RDS Multi-AZ vs Aurora Multi-AZ vs Aurora Global DB**

| Feature | RDS Multi-AZ | Aurora Multi-AZ | Aurora Global DB |
| ----- | ----- | ----- | ----- |
| Failover time | \~1-2 min | \< 30 sec | \< 1 min (regional failover) |
| Read from standby? | No | Yes (up to 15 Aurora Replicas) | Yes (local reads in each region) |
| Replication | Sync to 1 standby in same region | 6 copies in 3 AZs (shared volume) | Async to up to 5 secondary regions |
| RPO | Near zero (sync) | Near zero (sync writes confirmed in 4/6 copies) | \< 1 second (async) |
| Scope | Single region, 2 AZs | Single region, 3 AZs | Multi-region |
| Use for | HA within region | HA \+ reads within region | Global DR \+ local reads globally |

## **CloudWatch vs CloudTrail vs Config vs Trusted Advisor**

| Service | Question it Answers | Data Source | Memory Aid |
| ----- | ----- | ----- | ----- |
| CloudWatch | How is my application PERFORMING? | Metrics, logs from AWS services and applications | Watch \= performance monitoring |
| CloudTrail | WHO called what AWS API, WHEN? | AWS API call logs (management \+ data events) | Trail \= footprints (audit trail) |
| AWS Config | Is my infrastructure COMPLIANT with rules? | Configuration item history for every AWS resource | Config \= configuration compliance |
| Trusted Advisor | Am I following AWS BEST PRACTICES? | AWS analysis of your account | Advisor \= recommendations |

## **Cognito User Pools vs Identity Pools**

| Feature | User Pool | Identity Pool |
| ----- | ----- | ----- |
| Purpose | Handles user sign-up, sign-in, MFA, password reset | Exchanges tokens for temporary AWS credentials (STS) |
| Output | JWT tokens (ID token, access token, refresh token) | AWS credentials (Access Key ID \+ Secret \+ Session Token) |
| Who are the users? | Application users (your customers) | Any authenticated user (User Pool, Google, Facebook, SAML, guest) |
| AWS service access? | No (JWT is for your app) | Yes — gives access to AWS services (S3, DynamoDB, etc.) |
| Exam scenario | "user login for web/mobile app" | "users need direct access to S3 from mobile app" |

## **Direct Connect vs VPN vs PrivateLink vs Peering**

| Option | What it is | Use when |
| ----- | ----- | ----- |
| Site-to-Site VPN | Encrypted IPSec over public internet | Fast to set up, cost-sensitive, acceptable variable latency, \< 1.25 Gbps |
| Direct Connect | Private physical connection, no internet | Consistent performance, high bandwidth (1/10/100 Gbps), compliance, low latency |
| VPC Peering | Direct VPC-to-VPC private link | Connect two VPCs (same or different account/region); non-transitive; no overlapping CIDR |
| Transit Gateway | Central hub connecting many VPCs \+ on-prem | Scale beyond peering mesh; transitive routing; simplify hub-and-spoke network |
| PrivateLink | Expose one service to consumers without full VPC access | SaaS-to-customer access; one-way service exposure; no route tables needed |
| VPC Endpoints | Private access to AWS public services from VPC | Access S3/DynamoDB (Gateway) or other AWS services (Interface) without internet |

| SECTION 12 — PRACTICE QUESTIONS BY DOMAIN |
| :---: |

---

[< Other Important Services](23-other-services.md) | [Back to README](../README.md) | [Exam-Style Practice Questions >](25-practice-questions.md)
