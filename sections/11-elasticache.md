# **ElastiCache — Caching Strategies**

| Strategy | How it Works | Best For | Risk |
| ----- | ----- | ----- | ----- |
| Lazy Loading (Cache-Aside) | Check cache → miss → fetch from DB → write to cache | Read-heavy, tolerance for stale data | Cache miss penalty (3 trips); stale data if DB changes without cache update |
| Write-Through | Write to DB and cache simultaneously | Data freshness critical; small dataset | Write penalty (2 trips per write); cache churn if rarely read |
| Write-Behind (Write-Back) | Write to cache first; async write to DB | Write-heavy workloads | Data loss if cache fails before DB write |
| Cache TTL | Items expire after N seconds | Prevent stale data buildup | Too short \= cache misses; too long \= stale data |

| ⚠️ EXAM TRAP: Redis vs Memcached for the exam: If the question mentions ANY of these → choose Redis: persistence, pub/sub, Lua scripting, sorted sets (leaderboards), geospatial, replication, Multi-AZ, backups, or complex data structures. Memcached is only chosen for 'simple, stateless cache needing horizontal scale with multiple CPU cores.' |
| :---- |

|  SECTION 5 — NETWORKING: VPC, ROUTE 53, CLOUDFRONT & MORE |
| :---- |

---

[< DynamoDB - The Serverless NoSQL Giant](10-dynamodb.md) | [Back to README](../README.md) | [VPC - Virtual Private Cloud >](12-vpc.md)
