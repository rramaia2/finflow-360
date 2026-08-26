# Functional Requirements

## Authentication and authorization

- FR-001: The system shall authenticate interactive users using OAuth2.
- FR-002: The system shall authorize requests using JWT roles.
- FR-003: The system shall support CUSTOMER, OPERATIONS, AUDITOR, and ADMIN roles.

## Payments

- FR-004: The system shall allow an authorized user to submit a payment.
- FR-005: The system shall assign a unique transaction ID to every payment.
- FR-006: The system shall require an idempotency key.
- FR-007: The system shall not create multiple payments for the same key.
- FR-008: The system shall maintain payment-status history.
- FR-009: Customers shall only see their own payments.

## Settlement

- FR-010: The system shall publish accepted payments to Kafka.
- FR-011: The system shall process settlement asynchronously.
- FR-012: The system shall retry temporary settlement failures.
- FR-013: The system shall move exhausted failures to a DLQ.
- FR-014: Consumers shall safely handle duplicate events.

## Reconciliation

- FR-015: The system shall reconcile settled payments.
- FR-016: The system shall identify settlement mismatches.
- FR-017: Operations users shall review reconciliation exceptions.

## Operations

- FR-018: Operations users shall search for payments.
- FR-019: Authorized users shall retry eligible failed payments.
- FR-020: Every retry shall create an audit record.