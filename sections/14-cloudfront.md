# **CloudFront — Content Delivery Network**

CloudFront is AWS's global CDN. It caches content at 400+ edge locations worldwide and integrates deeply with AWS services.

## **CloudFront Key Concepts**

| Concept | Detail | Exam Implication |
| ----- | ----- | ----- |
| Origin | Where CloudFront fetches content from: S3, ALB, EC2, API Gateway, any HTTP server | S3 origin: use Origin Access Control (OAC) not OAI (legacy). ALB/EC2: must be publicly accessible or use VPC Origin. |
| Distribution | A CloudFront deployment with one or more origins and behaviors | One distribution can have multiple origins with different path patterns (e.g., /api/\* → ALB, /\* → S3) |
| Edge Location | 400+ global PoPs that cache content | Not the same as a Region or AZ |
| Cache Behaviors | Rules for how CloudFront caches and routes requests based on path patterns | Order matters — more specific paths should be listed first |
| TTL | Cache-Control and Expires headers control TTL; override in CloudFront behavior | Minimum TTL, Default TTL, Maximum TTL — CF uses min of max TTL and header value |
| OAC (Origin Access Control) | Grants CloudFront permission to access private S3 bucket; users cannot access S3 directly | Replace all OAI with OAC; prevents direct S3 URL access bypassing CloudFront |
| Signed URLs / Signed Cookies | Restrict content to authenticated users; signed with trusted key pair | Signed URL: one specific file. Signed Cookies: multiple files / membership access. |
| WAF Integration | AWS WAF on CloudFront protects globally at edge | Stops attacks before they reach origin; geo-blocking, rate limiting, SQL injection protection |
| Lambda@Edge / CloudFront Functions | Run code at edge: Lambda@Edge at regional edge (heavier), CF Functions at edge location (lighter) | Auth, A/B testing, URL rewrites. CF Functions: \< 1ms, \< 2MB. Lambda@Edge: up to 30s, 10GB RAM. |
| Field-Level Encryption | Encrypt specific POST fields (e.g. credit card) at edge; only specific origin servers can decrypt | PCI compliance, protect sensitive fields in transit beyond HTTPS |

| 💡 TIP: CloudFront vs S3 Transfer Acceleration: Both speed up S3 uploads/downloads using AWS edge network. CloudFront \= CDN for content delivery (reads primarily). S3 Transfer Acceleration \= upload acceleration via AWS backbone, specifically for S3 PUT operations from distant clients. |
| :---- |

| SECTION 6 — LOAD BALANCING: ALB, NLB, GWLB & ELB COMPARISON |
| :---: |

---

[< Route 53 - DNS and Routing Policies](13-route53.md) | [Back to README](../README.md) | [Elastic Load Balancing - Three Types Compared >](15-load-balancing.md)
