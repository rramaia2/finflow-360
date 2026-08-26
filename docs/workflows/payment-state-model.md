
stateDiagram-v2
    [*] --> RECEIVED
    RECEIVED --> PROCESSING
    RECEIVED --> VALIDATION_FAILED
    PROCESSING --> PENDING_SETTLEMENT
    PROCESSING --> SETTLEMENT_FAILED
    SETTLEMENT_FAILED --> PROCESSING: Retry
    PENDING_SETTLEMENT --> SETTLED
    SETTLED --> RECONCILED
    SETTLED --> RECONCILIATION_EXCEPTION
    RECONCILIATION_EXCEPTION --> RECONCILED: Resolved








| State | Meaning |
| --- | --- |
| RECEIVED | Payment has been accepted and stored |
| VALIDATION_FAILED | Payment failed business validation |
| PROCESSING | Payment is being processed |
| PENDING_SETTLEMENT | Payment was sent for settlement |
| SETTLED | Settlement completed successfully |
| SETTLEMENT_FAILED | Settlement could not be completed |
| RECONCILED | Payment and settlement records match |
| RECONCILIATION_EXCEPTION | Records require investigation |