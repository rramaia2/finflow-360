## US-001: Submit payment

As a customer,  
I want to submit a payment,  
so that the payment can be processed and settled.

### Acceptance criteria

- Given an authenticated customer
- When a valid payment is submitted
- Then the API returns HTTP 202
- And the response contains a transaction ID
- And the initial status is RECEIVED
- And a payment-created event is eventually published