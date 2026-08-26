# Initial Threat Model

| Threat | Example | Mitigation |
| --- | --- | --- |
| Spoofing | Stolen access token | Short-lived JWTs and signature validation |
| Tampering | Modified payment amount | Server validation and audit history |
| Repudiation | User denies retrying payment | Immutable audit event |
| Information disclosure | Account data appears in logs | Masking and structured logging |
| Denial of service | Excessive payment requests | API rate limiting and autoscaling |
| Privilege escalation | Customer invokes retry API | RBAC and endpoint authorization |
| Replay attack | Same request submitted repeatedly | Idempotency key |
| Duplicate event | Kafka redelivers message | Idempotent consumer |
| Secret exposure | Credentials committed to Git | Secret manager and scanning |

Public:
- Documentation
- Synthetic examples

Internal:
- System metrics
- Architecture configuration

Confidential:
- Customer identifiers
- Payment information
- Authentication records

Restricted:
- Credentials
- Private keys
- Access tokens