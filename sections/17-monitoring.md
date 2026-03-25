# **Monitoring Stack — CloudWatch, CloudTrail, Config**

| Service | What it monitors | What it stores | Exam Trigger Words |
| ----- | ----- | ----- | ----- |
| CloudWatch Metrics | Performance metrics (CPU, network, custom) | 15 months by default; detailed monitoring \= 1-min granularity | "monitor CPU", "set alarm", "auto scaling trigger" |
| CloudWatch Logs | Log ingestion from EC2, Lambda, RDS, VPC Flow Logs, etc. | Retain per log group (1 day to 10 years) | "centralize logs", "filter log events", "log insights query" |
| CloudWatch Alarms | Triggered when metric crosses threshold | Actions: SNS, Auto Scaling, EC2 action | "notify when CPU \> 80%", "scale when latency \> 500ms" |
| CloudWatch Events / EventBridge | React to AWS API events (cron schedule or event pattern) | Routes to targets (Lambda, SQS, etc.) | "trigger Lambda on schedule", "react to EC2 state change" |
| CloudTrail | AWS API calls (who did what when) | 90-day event history free; S3 for long-term | "audit API calls", "who deleted S3 bucket", "compliance trail" |
| AWS Config | Resource configuration changes \+ compliance rules | Configuration timeline; non-compliant alerts | "are resources compliant", "config drift", "remediation" |
| X-Ray | Distributed tracing for applications | Service maps, latency analysis, error analysis | "trace requests across microservices", "find bottleneck", "latency root cause" |
| AWS Health Dashboard | AWS service health events affecting your account | Alerts for maintenance, degradation, etc. | "notified when AWS maintenance affects my instances" |

| ⚠️ EXAM TRAP: CloudTrail vs CloudWatch: CloudTrail \= WHO called what API (audit). CloudWatch \= HOW is the system performing (metrics/logs). Config \= IS the resource compliant with rules (configuration state). These are three different questions. |
| :---- |

---

[< Messaging and Event-Driven Architecture](16-messaging.md) | [Back to README](../README.md) | [Security Services - Know Your Defense Layers >](18-security.md)
