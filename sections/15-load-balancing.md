# **Elastic Load Balancing — Three Types Compared**

Knowing WHICH load balancer to pick is a key SAA skill. The exam describes a requirement and expects you to match it.

| Feature | ALB (Application) | NLB (Network) | GWLB (Gateway) |
| ----- | ----- | ----- | ----- |
| OSI Layer | Layer 7 (HTTP/HTTPS/WebSocket/gRPC) | Layer 4 (TCP/UDP/TLS) | Layer 3+4 (IP packets) |
| Protocol | HTTP, HTTPS, WebSocket, gRPC | TCP, UDP, TLS | GENEVE (6081) for packet encapsulation |
| Performance | High throughput; some latency | Extreme performance; millions of req/sec; ultra-low latency | Transparent to traffic; used for appliances |
| Health checks | HTTP/HTTPS-based | TCP, HTTP, HTTPS | TCP, HTTP, HTTPS |
| Target types | EC2, IP, Lambda, containers | EC2, IP, ALB (as target) | EC2 instances running security appliances |
| Sticky sessions | Yes (application-based or duration-based cookies) | Yes (source IP) | No |
| WebSocket | Native support | Yes (Layer 4 pass-through) | N/A |
| Fixed IP | No (use NLB for fixed IP) | Yes (Elastic IP per AZ) | No |
| Use case | Web apps, microservices, content routing | TCP apps, gaming, IoT, NLB → ALB pattern | Deploy 3rd-party virtual appliances (Palo Alto, Fortinet) |
| Exam keyword | "HTTP routing", "host/path-based routing", "microservices", "Lambda" | "static IP", "TCP", "extreme performance", "UDP", "gaming" | "intrusion detection", "firewall appliance", "security inspection" |

| ⚠️ EXAM TRAP: NLB provides static IP addresses (one per AZ) — use this when clients need to whitelist fixed IPs. ALB has no fixed IPs. A common pattern: NLB in front of ALB to get fixed IPs while retaining Layer 7 routing. |
| :---- |

## **ALB Advanced Routing Features**

| Feature | Description | Example |
| ----- | ----- | ----- |
| Host-based routing | Route based on HTTP Host header | api.example.com → API Target Group; app.example.com → App Target Group |
| Path-based routing | Route based on URL path | /images/\* → Image servers; /api/\* → API servers |
| HTTP header routing | Route based on any HTTP header value | User-Agent: iPhone → mobile backend |
| HTTP method routing | Route based on GET/POST/PUT etc. | POST /orders → Order service TG |
| Query string routing | Route based on query string parameters | ?platform=mobile → Mobile TG |
| Fixed response | Return HTTP 200/301/302 directly from ALB | Maintenance page, redirects |
| Redirect action | ALB redirects HTTP → HTTPS | Enforce HTTPS without backend code |
| Lambda target | ALB invokes Lambda directly as target | Serverless web apps behind ALB |

## **Connection Draining / Deregistration Delay**

**What it is:** When an instance is deregistered or marked unhealthy, existing connections are kept alive for up to 3600 seconds (default 300 seconds) to complete in-flight requests before the instance is removed.

**Exam tip:** If the question says 'long-running uploads are being interrupted during deployments' → increase deregistration delay. If it says 'deployments are slow because instances stay in draining state too long' → decrease the delay.

| NEXT: SECTION 7 — MESSAGING: SQS, SNS, EVENTBRIDGE, KINESIS & MORE |
| :---: |

---

[< CloudFront - Content Delivery Network](14-cloudfront.md) | [Back to README](../README.md) | [Messaging and Event-Driven Architecture >](16-messaging.md)
