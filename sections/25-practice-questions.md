# **Exam-Style Practice Questions (But Without MCQs, think think think!!!)**

## **Domain 1: Design Resilient Architectures**

### **Q1**

**Question:** A company runs a critical e-commerce application on a single EC2 instance with an attached EBS volume. They want to achieve a recovery time objective (RTO) of under 5 minutes and a recovery point objective (RPO) of under 1 minute. What should a solutions architect recommend?

| 📌 NOTE: Think about what provides BOTH fast failover AND near-zero data loss before reading the answer below. |
| :---- |

**Answer:** Deploy a Multi-AZ RDS instance for the database (synchronous replication → RPO near-zero). Move the application to an EC2 Auto Scaling Group with a minimum of 2 instances across 2 AZs behind an ALB. Use Amazon Aurora instead of RDS if sub-30-second failover is needed. The ALB health checks will route around an unhealthy instance within seconds (RTO \< 5 min).

### **Q2**

**Question:** A startup stores user-uploaded images in S3. As the company grows, they need to serve images with low latency to global users, while protecting the S3 bucket from direct public access. What is the most appropriate solution?

**Answer:** Create a CloudFront distribution with an S3 origin. Enable Origin Access Control (OAC) on the CloudFront distribution and update the S3 bucket policy to allow access only from CloudFront's service principal. Disable Block Public Access settings that would conflict, but block all direct S3 access. This ensures users access content through CloudFront (low latency via edge caching) and cannot bypass it to access S3 directly.

### **Q3**

**Question:** A financial application requires database transactions that update multiple DynamoDB tables atomically — either all succeed or all fail. The application processes 2,000 transactions per second with peaks of 10,000. Which approach should the architect choose?

**Answer:** Use DynamoDB Transactions (TransactWrite) for atomic multi-table operations. Configure DynamoDB with On-Demand capacity mode to handle variable throughput without capacity planning. DynamoDB Transactions consume 2 WCUs per item write (vs 1 normally) — factor this into capacity. The On-Demand mode automatically scales for the 5x peak without throttling.

## **Domain 2: Design High-Performing Architectures**

### **Q4**

**Question:** A media streaming company needs to ingest 1 TB of clickstream data per hour from 10,000 simultaneous users and run real-time analytics to detect trending content. Which architecture handles this?

**Answer:** Use Kinesis Data Streams to ingest clickstream events in real time (provision enough shards: at 1 MB/s per shard, \~280 shards for \~280 MB/s). Use Kinesis Data Analytics (Apache Flink) to run real-time aggregations on the stream to detect trending content. Write results to DynamoDB for low-latency serving. Simultaneously use Kinesis Data Firehose to deliver raw data to S3 for long-term analytics with Athena.

### **Q5**

**Question:** A web application experiences slow database response times during peak hours due to repetitive read queries for the same product catalog data. The data changes at most once per hour. What is the most cost-effective solution?

**Answer:** Implement ElastiCache for Redis with a lazy loading (cache-aside) pattern. On cache miss, load from RDS and cache with TTL of 3600 seconds (1 hour). For the cache to be most effective, also add Read Replicas to RDS to distribute any remaining cache-miss load. This is more cost-effective than upgrading the RDS instance class.

## **Domain 3: Design Secure Architectures**

### **Q6**

**Question:** A company is deploying an application that stores sensitive customer PII in S3. They need to: (1) automatically discover what PII exists, (2) encrypt the data, (3) detect unusual access patterns, and (4) audit all access to the data. Which combination of services achieves all four?

**Answer:** (1) Amazon Macie — automatically discovers and classifies PII/sensitive data in S3. (2) S3 SSE-KMS encryption with customer-managed CMK — encrypts data and provides audit trail of decryption. (3) Amazon GuardDuty — uses ML to detect anomalous S3 access patterns. (4) AWS CloudTrail with S3 data events enabled — logs every GetObject, PutObject call with user identity, time, and source IP.

### **Q7**

**Question:** An EC2 instance in a private subnet needs to call the DynamoDB API. The company wants to ensure traffic never traverses the public internet and they do not want to pay for NAT Gateway data transfer charges. What should the architect configure?

**Answer:** Create a VPC Gateway Endpoint for DynamoDB. Gateway Endpoints are free, route traffic through the AWS network (no internet), and require updating the route table to direct DynamoDB traffic through the endpoint. This is more cost-effective than routing through a NAT Gateway, which charges for data processed.

## **Domain 4: Design Cost-Optimized Architectures**

### **Q8**

**Question:** A data analytics company runs large Apache Spark jobs nightly that process log files stored in S3. Each job runs for 3-4 hours and can be restarted if interrupted. They want the most cost-effective compute solution.

**Answer:** Use Amazon EMR with Spot Instances for task nodes (they do the heavy lifting) and On-Demand instances for the master and core nodes (they must not be interrupted). Spot Instances can save up to 90% over On-Demand. Since the jobs can tolerate interruption and restart (fault-tolerant batch processing), Spot is ideal. Use EMR Instance Fleets or Instance Groups with multiple Spot pools for better availability.

### **Q9**

**Question:** A company stores 100 TB of log files in S3 Standard. The logs are accessed frequently in the first 30 days, rarely between 30-90 days, and almost never after 90 days. After 365 days, they must retain logs for compliance but retrievals can take up to 12 hours. Design the most cost-effective S3 strategy.

**Answer:** Create an S3 Lifecycle Policy: (1) Day 0-30: S3 Standard (frequent access). (2) Day 30-90: Transition to S3 Standard-IA (infrequent access, milliseconds retrieval). (3) Day 90-365: Transition to S3 Glacier Flexible Retrieval (archives, 1min-12hrs retrieval, 90-day minimum billing period satisfied). (4) Day 365+: Transition to S3 Glacier Deep Archive (12-48hr retrieval, cheapest for compliance retention). This progressively reduces cost as access frequency drops.

### **Q10**

**Question:** A company runs a three-tier web application with ALB, EC2 application servers, and RDS MySQL. Traffic is highly predictable: 8 AM to 6 PM weekdays at full load, negligible overnight and weekends. What purchasing strategy minimizes cost while maintaining performance?

**Answer:** For EC2: Use scheduled Auto Scaling to scale in/out the ASG based on time. Purchase Reserved Instances (1-year Standard) for the minimum baseline capacity (overnight/weekend level). The peak capacity above baseline should use On-Demand (no commitment needed for predictable but variable peak). For RDS: Multi-AZ Reserved Instance (1-year) for the MySQL instance — RDS runs 24/7 regardless of traffic, so Reserved provides the best savings.

| SECTION 13 — CATEGORY SUMMARIES & QUICK REFERENCE |
| :---: |

---

[< Most-Confused Services and Concepts](24-common-confusions.md) | [Back to README](../README.md) | [Summary: Service Selection by Problem Type >](26-summary-quick-reference.md)
