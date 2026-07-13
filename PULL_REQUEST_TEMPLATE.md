## Summary
<!-- What does this PR do? Link the issue it resolves. -->

Closes #{issue_number}

## Changes
<!-- Brief bullet list of what changed -->
- 

## Testing
<!-- How did you test this? Include relevant test output. -->

```
cargo test -- --nocapture   # contract tests
npm test                    # backend tests
```

## Contract changes
<!-- If you modified a Soroban contract, answer these: -->
- [ ] New/changed contract functions have unit tests
- [ ] `cargo clippy -- -D warnings` passes
- [ ] `cargo fmt` applied
- [ ] No new `unwrap()` without error handling

## Backend/frontend changes
- [ ] Zod validation added for new request bodies
- [ ] `npm run type-check` passes
- [ ] New endpoints documented (or existing docs updated)

## Checklist
- [ ] I have read CONTRIBUTING.md
- [ ] Tests pass locally (`make test`)
- [ ] I have self-reviewed this PR
- [ ] No secrets or sensitive data in commits

## Stellar Wave (if applicable)
- Applied on Drips at: <!-- drips.network link -->
