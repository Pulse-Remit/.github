# Real cross-contract call from RemittanceRouter to registered pools

**Complexity**: High

## Summary

`RemittanceRouter.send_remittance()` currently *simulates* the cross-currency swap output using a hardcoded approximation (`(amount * 997) / 1000`, i.e. an assumed flat 0.3% pool fee) rather than actually invoking the registered pool contract. The pool address is correctly looked up via `register_pool()` / storage, but the swap itself is never executed against it.

**Important — read before starting**: an earlier version of this issue asked for routing via Stellar's classic path-payment operation (`pathPaymentStrictSend`). That is not possible — Soroban contracts cannot invoke the Stellar classic DEX, order book, or path payment operations under any circumstances; this is a Soroban runtime constraint, not a missing feature. See [`pulse-remit-docs/architecture/system-overview.md`](https://github.com/YOUR_ORG/pulse-remit-docs/blob/main/architecture/system-overview.md) and [`contract-reference.md`](https://github.com/YOUR_ORG/pulse-remit-docs/blob/main/contracts/contract-reference.md#why-registered-pools-not-the-sdex) for the full explanation. This issue is specifically about wiring a real **cross-contract call to the registered Soroban pool**, which is the correct and only viable mechanism.

## What needs to be done

1. In `send_remittance()`, after determining the registered pool address for `(source_token, dest_token)`, use `env.invoke_contract()` to call that pool's `swap_a_for_b()` (or `swap_b_for_a()`, depending on token order) function directly, rather than approximating the output locally.
2. Pass `min_received` through as the pool call's own slippage guard, so the pool itself enforces the guard rather than only `RemittanceRouter` checking it after the fact.
3. Handle the case where the registered pool's interface doesn't match the expected `swap_a_for_b(from, amount_in, min_out) -> i128` signature gracefully (a clear panic with a descriptive error, not a silent failure).
4. Add an integration-style unit test that registers a real deployed `StableSwap` instance (from this same repository) as the pool and verifies the actual swapped amount matches what `StableSwap.quote_a_for_b()` predicted beforehand.

## Acceptance criteria

- [ ] `send_remittance()` makes a real `env.invoke_contract()` call to the registered pool instead of approximating the swap output
- [ ] `min_received` is enforced by the actual pool call, not just a local approximation check
- [ ] New test: registers a real `StableSwap` pool, executes a cross-currency remittance, and asserts the received amount matches the pool's own quote
- [ ] Existing tests continue to pass unchanged
- [ ] No reference to Stellar path payments or the classic DEX is reintroduced anywhere in this contract

## Stellar Wave

Points: 200 | Complexity: High
