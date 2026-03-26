# **RDS — Relational Database Service**

## **RDS Multi-AZ vs Read Replicas — The Classic Confusion**

| Feature | Multi-AZ | Read Replica |
| ----- | ----- | ----- |
| Purpose | HIGH AVAILABILITY (failover) | PERFORMANCE (read scaling) |
| Replication | Synchronous — standby always in sync | Asynchronous — slight lag possible |
| Readable? | NO — standby is passive; only used during failover | YES — serve read traffic |
| Failover time | \~1-2 minutes (automatic DNS flip) | Must manually promote to primary (not automatic) |
| Cross-region? | Only within same region | Can be cross-region (for disaster recovery) |
| Cross-AZ cost? | Free data transfer for Multi-AZ replication | Cross-region replica has data transfer cost |
| Exam keyword | "availability", "failover", "disaster recovery" | "performance", "read traffic", "reporting", "analytics" |

| ⚠️ EXAM TRAP: CRITICAL: Multi-AZ does NOT improve read performance — the standby is not readable. If a question says 'improve read performance AND high availability,' the answer uses BOTH Multi-AZ AND Read Replicas. |
| :---- |

## **RDS Backup & Restore**

| Feature | Details |
| ----- | ----- |
| Automated Backups | Daily snapshot \+ transaction logs → point-in-time restore (PITR) up to 35 days. Stored in S3. |
| Manual Snapshots | User-initiated; retained indefinitely (until you delete). Shared across regions/accounts. |
| Restore behavior | Always creates a NEW DB instance — you cannot restore in-place. Update app connection string. |
| RDS Backup window | Configure during low-traffic period. I/O may be briefly suspended for single-AZ. |
| Deletion protection | Enable to prevent accidental deletion. Must disable before terminating. |


---

[< Database Selection Guide](07-database-selection.md) | [Back to README](../README.md) | [Aurora - The Exam Favorite >](09-aurora.md)
