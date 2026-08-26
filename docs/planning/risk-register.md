# Risk Register

| ID | Risk | Probability | Impact | Mitigation |
| --- | --- | --- | --- | --- |
| R-001 | Duplicate payment processing | Medium | Critical | Idempotency key and database constraint |
| R-002 | Database commit without Kafka event | Medium | Critical | Transactional outbox |
| R-003 | Duplicate Kafka event | High | High | Idempotent consumers |
| R-004 | Settlement provider outage | Medium | High | Timeout, retry, circuit breaker and DLQ |
| R-005 | Out-of-order events | Medium | High | Account partitioning and state validation |
| R-006 | Sensitive information in logs | Medium | Critical | Log masking and reviews |
| R-007 | Excessive consumer lag | Medium | High | Alerts and consumer autoscaling |
| R-008 | Unauthorized retry | Low | Critical | RBAC and audit history |
| R-009 | Defective deployment | Medium | High | Canary deployment and rollback |