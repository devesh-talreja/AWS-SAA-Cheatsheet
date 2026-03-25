# **AWS Lambda**

Lambda runs code without provisioning servers. The exam tests you on limits, triggers, integrations, and when NOT to use Lambda.

## **Lambda Key Facts for the Exam**

| Property | Limit / Detail |
| ----- | ----- |
| Max execution timeout | 15 minutes (900 seconds) |
| Max memory | 128 MB to 10,240 MB (10 GB); CPU scales proportionally with memory |
| Max deployment package | 50 MB (zip), 250 MB (unzipped), 10 GB (container image) |
| Max /tmp storage | 10 GB (was 512 MB until 2023 increase) |
| Concurrent executions (default) | 1,000 per region (soft limit; can be increased) |
| Reserved concurrency | Guarantees N executions for one function; reduces pool for others |
| Provisioned concurrency | Pre-warms instances to eliminate cold starts — costs extra |
| Event sources (triggers) | S3, DynamoDB Streams, Kinesis, SQS, SNS, EventBridge, API Gateway, ALB, Cognito, etc. |
| Pricing | Per request ($0.20/million) \+ per GB-second of compute |

## **Lambda vs EC2 — When to Choose Each**

| Choose Lambda When... | Choose EC2 When... |
| ----- | ----- |
| Event-driven, sporadic traffic | Continuously running processes |
| Tasks under 15 minutes | Long-running jobs (\> 15 min) |
| No server management desired | Full OS control needed |
| Variable/unpredictable load | Predictable steady-state load (Reserved Instances save money) |
| Simple stateless functions | Stateful applications with local storage needs |

## **Lambda Destinations & Error Handling**

**Asynchronous Lambda:** Lambda retries twice on failure automatically. You can configure an on-success and on-failure destination (SQS, SNS, EventBridge, another Lambda). This is the modern replacement for Dead Letter Queues (DLQs), though DLQs still work.

| 💡 TIP: For SQS triggers: Lambda polls SQS and processes up to 10 messages per batch. On failure, messages return to the queue (up to maxReceiveCount), then go to DLQ. Use partial batch response to report only failed messages. |
| :---- |

---

[< EC2 - Elastic Compute Cloud](02-ec2.md) | [Back to README](../README.md) | [Containers on AWS: ECS, EKS, Fargate >](04-containers.md)
