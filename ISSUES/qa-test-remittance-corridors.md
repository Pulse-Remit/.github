# 🧪 QA: Manual testing of remittance corridor fee estimates

**Labels**: `QA`, `good first issue`, `testing`, `help wanted`
**Complexity**: 🟢 Beginner — browser testing, no coding needed

## Summary
The `/send` page and `/api/v1/remittances/corridors/supported` endpoint return fee estimates for five corridors. These need to be manually tested to verify the UI correctly shows fee amounts and recipient calculations.

## What needs to be done
Test the following scenarios in a running local dev environment (see README quickstart) and document your findings:

### Corridor tests
For each of the 5 corridors (NG-KE, NG-GH, MX-US, PH-US, IN-AE):
1. Navigate to `/send`, select the corridor
2. Enter amounts: 10, 100, 500, 1000, 5000 USDC
3. Verify fee amount = amount × (feeBps / 10000)
4. Verify "Recipient gets" = amount - fee
5. Verify UI shows all values correctly

### Edge case tests
- [ ] Amount of 0 → should show validation error
- [ ] Amount of 0.001 → how does UI handle very small amounts?
- [ ] No corridor selected → "Send" button should be disabled
- [ ] Recipient wallet field: 55 chars → validation error; 56 chars → accepted; 57 chars → validation error
- [ ] Sender and recipient same address → document what happens

## Deliverable
Create `docs/qa/corridor-test-report.md` with a table of results. For any bug found, open a separate GitHub issue linking this one.

## Acceptance criteria
- [ ] Test report covers all 5 corridors × 5 amounts = 25 cases
- [ ] All edge cases documented
- [ ] Any bugs found are opened as new issues
- [ ] PR adds the report at `docs/qa/corridor-test-report.md`

## Stellar Wave
Points: 60 | Complexity: 🟢 Beginner — QA testers and non-devs welcome
