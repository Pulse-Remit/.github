# Add salary advance UI to employee dashboard

**Complexity**: medium

## Summary
The `PayrollVault.request_advance()` contract function is implemented but the dashboard has no UI for it. Add an "Request Advance" button on the employee detail view.

## Acceptance criteria
- [ ] Advance button visible when employee has `advance_pct > 0`
- [ ] Shows estimated advance amount
- [ ] Calls `POST /api/v1/employees/:id/advance` (new endpoint needed)
- [ ] Disables button after successful request (once per cycle)

## Stellar Wave
Points: 150 | Complexity: 🟡 Medium
