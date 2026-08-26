# Nonfunctional Requirements

| ID | Category | Requirement | Verification |
| --- | --- | --- | --- |
| NFR-001 | Performance | p95 API latency shall remain below 200 ms | Load test |
| NFR-002 | Capacity | System shall support 50,000 simulated payments per day | Load test |
| NFR-003 | Availability | Production-like target shall be 99.9% | Monitoring |
| NFR-004 | Reliability | Accepted payments shall not be silently lost | Failure test |
| NFR-005 | Idempotency | Duplicate keys shall not create duplicate payments | Integration test |
| NFR-006 | Ordering | Events for one account shall preserve ordering | Kafka test |
| NFR-007 | Security | Sensitive APIs shall require OAuth2/JWT | Security test |
| NFR-008 | Authorization | Retry operations shall require OPERATIONS role | Authorization test |
| NFR-009 | Observability | Requests and events shall include correlation IDs | Log validation |
| NFR-010 | Quality | Backend unit-test coverage shall be at least 90% | SonarQube |
| NFR-011 | Recovery | Application rollback shall complete within 15 minutes | Deployment drill |
| NFR-012 | Scalability | API and consumers shall scale independently | Kubernetes test |