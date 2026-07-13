# Stellar event indexer: persist wage claims

**Complexity**: medium

## Summary
The indexer (`src/indexers/stellar.indexer.ts`) processes `wages_claimed` events but only logs them. It must upsert a `WageClaim` row in PostgreSQL with the employee address, amount, cycle count, and ledger timestamp.

## Acceptance criteria
- [ ] `handleWagesClaimed()` parses the event value Vec (employee, amount, cycles)
- [ ] Inserts/updates `WageClaim` row via Prisma
- [ ] `GET /api/v1/employees/:id/claims` returns the persisted records
- [ ] Test: mock event triggers DB write

## Stellar Wave
Points: 150 | Complexity: 🟡 Medium
