# Wire Freighter signing into the send and claim transaction flows

**Complexity**: Medium

## Summary
The `useWallet()` hook (`pulse-remit-frontend/hooks/useWallet.ts`) already implements Freighter connection, address retrieval, and a `sign(xdr)` method. What's still missing is the code that *builds* the actual Soroban transaction XDR for the two flows that need a real signature: sending a remittance and claiming wages. Right now those actions go through the backend API only; they don't yet build a client-side transaction for the user to sign directly.

## What needs to be done

1. Add a `lib/stellar.ts` utility exporting functions that build unsigned transaction XDR for:
   - `RemittanceRouter.send_remittance(...)` — used on `/send`
   - `PayrollVault.claim_wages(...)` — used on `/dashboard`
2. Update the `/send` page's submit handler to: build the transaction via the new utility, call `sign(xdr)` from `useWallet()`, then submit the signed XDR to Stellar RPC directly (or to a new backend endpoint that just relays the already-signed XDR — do not have the backend sign on the user's behalf).
3. Update the `/dashboard` page's "Claim Wages" button with the same pattern for `claim_wages`.
4. Handle the three realistic failure states in the UI: wallet not connected, user rejects the signature request in Freighter, and Soroban RPC submission failure (e.g. insufficient balance, expired transaction).

## Acceptance criteria

- [ ] `lib/stellar.ts` builds valid unsigned XDR for both operations, verified against a real testnet submission
- [ ] `/send` page signs with the connected wallet, not a backend-held key
- [ ] `/dashboard` claim flow signs with the connected wallet
- [ ] All three failure states show a clear, distinct message to the user
- [ ] No regression to the existing `useWallet()` hook's connect/disconnect behavior

## Stellar Wave

Points: 150 | Complexity: Medium
