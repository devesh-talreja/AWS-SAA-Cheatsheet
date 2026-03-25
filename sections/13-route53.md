# **Route 53 — DNS & Routing Policies**

Route 53 is AWS's DNS service. The SAA exam tests routing policies extensively — know which policy to pick in each scenario.

## **Route 53 Routing Policies**

| Policy | How it Works | Use Case | Exam Scenario Keyword |
| ----- | ----- | ----- | ----- |
| Simple | Maps domain to one or more resources; random selection if multiple values | Single resource or stateless one-backend | "basic DNS", "single endpoint" |
| Weighted | Split traffic by weights (0-255); weight 0 \= no traffic | A/B testing, blue/green deployments, gradual migration | "split 10% to new version", "blue/green", "canary" |
| Latency-based | Routes to region with lowest network latency for user | Multi-region app, global users wanting fast response | "lowest latency", "fastest response for users globally" |
| Failover | Active-Passive; routes to secondary when primary health check fails | Disaster recovery, active-standby architecture | "failover", "DR", "primary fails → secondary" |
| Geolocation | Routes based on user's geographic location (continent, country, state) | Content localization, GDPR data residency, language routing | "users in Europe to EU servers", "data residency", "localization" |
| Geoproximity | Routes based on location \+ optional bias to shift traffic toward/away from a region | Fine-grained geographic traffic shifts; expand/shrink region coverage | "shift more traffic to new region", "traffic engineering by geography" |
| Multi-Value Answer | Returns up to 8 healthy records (like Simple \+ health checks) | Client-side load balancing across multiple endpoints | "simple load balancing", "up to 8 endpoints", "NOT a replacement for ELB" |
| IP-Based | Routes based on client IP CIDR blocks you define | Route ISP traffic to specific endpoints, cost optimization | "route specific IP ranges", "ISP-based routing" |

| ⚠️ EXAM TRAP: Geolocation vs Geoproximity: Geolocation is STRICT (users from France go to EU endpoint — full stop). Geoproximity uses location \+ BIAS to expand or shrink a region's effective coverage area — it's about TRAFFIC ENGINEERING, not strict regional routing. |
| :---- |

## **Route 53 Health Checks**

| Type | What it Checks |
| ----- | ----- |
| Endpoint Health Check | HTTP/HTTPS/TCP check to a specific IP or hostname; 15 global checkers; 3/5 threshold for pass/fail |
| Calculated Health Check | Aggregate multiple health checks with AND/OR logic; parent health based on child checks |
| CloudWatch Alarm | Health based on CW metric/alarm state — use this for private resources (no internet access) |

---

[< VPC - Virtual Private Cloud](12-vpc.md) | [Back to README](../README.md) | [CloudFront - Content Delivery Network >](14-cloudfront.md)
