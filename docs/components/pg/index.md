---
title: Payment Gateway
---

# Payment Gateway


<https://github.com/unicef/hope-payment-gateway>

Component to integrate with external FSP: e.g. Western Union

The Integration between HOPE and any FSP (we are starting with Western Union) is performed through a middleware service called Payment Gateway (PG).
HOPE sends to the PG informations regarding Payment Plan and related payments through web API.
Each FSP can have a different way to interact with the payment gateway with though strategy pattern.

## HOPE / PG Integration API

PG expose endpoint to accept:

- Payment Plan creation
- Add Records to Payment Plan
- Payment Plan ready
- Status of payments given a Payment Plan


## Statues

### Payment Plan

- Draft
- Open
- Ready
- Closed
- Aborted
- Processed

### Payment Record

- Pending
- Transferred to FSP
- Transferred to Beneficiary
- Cancelled
- Refund
- Purged
- Error

## Western Union

Once HOPE confirms that Payment Plan is ready, PG starts sending data to Western Union though SOAP Requests.

Transactions support:

- Money in Minutes (aka Cash by FSP)
- Wallets (aka Mobile Money)
