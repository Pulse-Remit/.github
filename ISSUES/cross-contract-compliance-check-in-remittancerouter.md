# Cross-contract compliance check in RemittanceRouter

**Complexity**: high

## Summary
`RemittanceRouter.send_remittance()` currently does not enforce a pre-flight compliance check. Before routing a payment, the contract must call `ComplianceRegistry.is_clear(sender)` and `ComplianceRegistry.is_clear(recipient)` via cross-contract invocation.

## Acceptance criteria
- [ ] `send_remittance()` calls `ComplianceRegistry.is_clear(sender)` before executing
- [ ] `send_remittance()` calls `ComplianceRegistry.is_clear(recipient)` before executing
- [ ] Returns new error `PaymentBlockedByCompliance` if either check fails
- [ ] Unit test: blocked sender cannot remit
- [ ] Unit test: blocked recipient cannot receive

## Technical notes
Use `soroban_sdk::invoke_contract` to make the cross-contract call.
See `contracts/compliance_registry/src/lib.rs` for the `is_clear()` function signature.

## Stellar Wave
Points: 200 | Complexity: 🔴 High
