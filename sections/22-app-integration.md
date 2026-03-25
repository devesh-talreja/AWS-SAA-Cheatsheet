# **Application Integration & Orchestration**

| Service | Purpose | Key Facts |
| ----- | ----- | ----- |
| Step Functions | Serverless workflow orchestration (state machine) | Visual workflows; Standard (1-year duration; async) vs Express (5-min; IoT/streaming); error handling, retries, parallel states |
| AppFlow | No-code SaaS data integration | Salesforce, ServiceNow, Slack → S3, Redshift; scheduled or event-driven; field-level encryption in transit |
| API Gateway | Managed API endpoint (REST, HTTP, WebSocket) | Throttling; caching; API keys; usage plans; mock integration; Cognito/Lambda authorizers |
| AWS AppSync | Managed GraphQL service | Real-time data sync; subscriptions (WebSocket); resolvers to DynamoDB, Lambda, HTTP; for mobile/web apps |
| SWF (Simple Workflow Service) | Workflow orchestration (legacy) | Prefer Step Functions; SWF used when you need human approval steps or external process integration via long-running tasks |

---

[< Analytics Services](21-analytics.md) | [Back to README](../README.md) | [Other Important Services >](23-other-services.md)
