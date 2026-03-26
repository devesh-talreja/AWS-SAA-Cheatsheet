# **Security Services — Know Your Defense Layers**

| Service | What it Does | Layer | Exam Scenario |
| ----- | ----- | ----- | ----- |
| AWS WAF | Web Application Firewall; rules against SQL injection, XSS, bad bots, geo-blocks | Layer 7; CloudFront, ALB, API GW, AppSync | "block SQL injection", "protect against OWASP Top 10", "geo-block countries" |
| AWS Shield Standard | Automatic DDoS protection (Layers 3/4) for all AWS customers at no cost | Layer 3/4; all resources | Always on; no configuration needed |
| AWS Shield Advanced | $3,000/month; Enhanced DDoS protection \+ 24/7 DDoS Response Team \+ cost protection | Layer 3/4/7; CloudFront, Route53, ALB, NLB, EIP | "sophisticated DDoS attacks", "financial protection", "DRT support" |
| AWS Firewall Manager | Centrally deploy and manage WAF rules, Shield Advanced, SGs, Network Firewall across org | Multi-account, Organizations-level | "apply WAF rules across all accounts", "organization-wide security policies" |
| Amazon GuardDuty | Threat detection using ML on CloudTrail, VPC Flow Logs, DNS Logs, S3 logs, EKS logs | Account-level threat intelligence | "detect cryptomining", "suspicious API calls", "unauthorized access" |
| Amazon Inspector | Automated vulnerability assessment for EC2, ECR images, Lambda functions | Workload-level CVEs | "scan EC2 for vulnerabilities", "container image scanning", "CVE detection" |
| Amazon Macie | ML-based PII/sensitive data discovery and classification in S3 | Data classification | "find PII in S3", "GDPR compliance", "sensitive data discovery" |
| AWS Security Hub | Aggregates findings from GuardDuty, Inspector, Macie, Config into unified dashboard | Cross-service aggregation | "single pane of glass for security", "normalize findings" |
| AWS Network Firewall | Managed stateful firewall (Suricata rules) for VPC — deep packet inspection | VPC level | "deep packet inspection", "IDS/IPS in VPC", "custom domain filtering" |
| Secrets Manager | Store, rotate, retrieve secrets (DB passwords, API keys); auto-rotation with Lambda | Application secrets | "rotate DB credentials automatically", "never hardcode passwords" |
| Systems Manager Parameter Store | Store config data and secrets (standard: free, advanced: $0.05/param/month) | Config & secrets | "store configuration", "free secrets storage", "hierarchy config" |
| KMS (Key Management Service) | Create and manage encryption keys; integrate with 100+ AWS services | Encryption key management | "customer managed keys", "key rotation", "envelope encryption" |
| CloudHSM | Dedicated Hardware Security Module; you manage keys entirely; FIPS 140-2 Level 3 | Hardware key protection | "FIPS 140-2 Level 3", "full key control", "regulatory compliance (PKCS11, JCE)" |

| ⚠️ EXAM TRAP: Secrets Manager vs Parameter Store: Secrets Manager costs \~$0.40/secret/month but auto-rotates credentials and is designed for secrets. Parameter Store is free for standard parameters but no auto-rotation (need to trigger Lambda yourself). For exam: 'auto-rotate database credentials' → Secrets Manager. |
| :---- |

| 🧠 MNEMONIC: GuardDuty \= Guard dog (threat DETECTION). Inspector \= Home inspector (vulnerability SCANNING). Macie \= Mac & Privacy (PII/data CLASSIFICATION). These are three different jobs: detect threats, find vulnerabilities, classify data. |
| :---- |

| NEXT: SECTION 9 — ARCHITECTURAL PATTERNS & DESIGN DECISIONS |
| :---: |

---

[< Monitoring Stack - CloudWatch, CloudTrail, Config](17-monitoring.md) | [Back to README](../README.md) | [Core Architectural Patterns for SAA >](19-architectural-patterns.md)
