# **DynamoDB — The Serverless NoSQL Giant**

DynamoDB is deeply integrated across AWS. Know its consistency models, capacity modes, indexing, and streams cold.

## **DynamoDB Core Concepts**

| Concept | Detail | Exam Implication |
| ----- | ----- | ----- |
| Primary Key | Can be simple (Partition Key only) or composite (Partition Key \+ Sort Key) | Design partition key for uniform distribution — avoid hot partitions |
| Read Consistency | Eventually Consistent (default, cheaper, 0.5 RCU per 4KB) or Strongly Consistent (1 RCU per 4KB) | Financial apps needing latest data → Strongly Consistent; extra 2x RCU cost |
| Capacity Modes | Provisioned (specify RCU/WCU; predictable cost) vs On-Demand (pay per request; variable load) | On-Demand for unpredictable; Provisioned \+ Auto Scaling for steady with spikes |
| DynamoDB Streams | Ordered stream of item changes (24-hour retention); triggers Lambda, Kinesis | Event-driven patterns: change data capture, cross-region replication, triggers |
| TTL (Time to Live) | Automatically delete items after timestamp expires; no cost for deletions | Session expiry, log retention, ephemeral data |
| DynamoDB Accelerator (DAX) | Write-through in-memory cache; microsecond read latency; no app code changes for reads | DAX is for read caching. DAX caches individual item reads and query results. |
| Global Tables | Multi-region, multi-active replication; DynamoDB Streams must be enabled | Active-active replication: write to any region, read from nearest |
| Transactions | ACID transactions across multiple items/tables using TransactWrite and TransactGet | Financial apps, order management, inventory systems |

## **DynamoDB Indexes**

| Index Type | Created When | Key Structure | Read Consistency | Throughput | Use Case |
| ----- | ----- | ----- | ----- | ----- | ----- |
| LSI (Local Secondary Index) | Table creation ONLY | Same partition key, different sort key | Strongly consistent OK | Shares table's provisioned capacity | Query same PK with different sort order |
| GSI (Global Secondary Index) | Any time | Different partition and/or sort key | Eventually consistent ONLY | Has its own provisioned capacity | Query on any attribute; most flexible |

| 🧠 MNEMONIC: LSI \= Local \= Same partition key \= created at table Launch. GSI \= Global \= Greater flexibility \= can be added anytime, own capacity. |
| :---- |

---

[< Aurora - The Exam Favorite](09-aurora.md) | [Back to README](../README.md) | [ElastiCache - Caching Strategies >](11-elasticache.md)
