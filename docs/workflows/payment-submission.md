# Payment Submission Workflow

## Preconditions

- The caller is authenticated.
- The caller has permission to create payments.
- The request contains an idempotency key.

## Main flow

1. The customer submits a payment.
2. API Gateway forwards the request to the Payment API.
3. The Payment API validates the JWT.
4. The API validates the amount, currency, account, and required fields.
5. The service searches for the idempotency key.
6. If the key is new, the payment is stored with RECEIVED status.
7. A payment-created outbox event is stored in the same transaction.
8. The API returns the transaction ID.
9. The outbox publisher sends the event to Kafka.
10. The Settlement Service consumes the event.

## Alternative flows

### Duplicate request

The API returns the original transaction instead of creating another payment.

### Invalid request

The API returns a validation error without publishing an event.

### Kafka unavailable

The payment remains stored, and the outbox publisher retries publication.

## Postconditions

- Exactly one payment exists for an idempotency key.
- The payment has an immutable status-history record.
- A payment-created event is eventually published.