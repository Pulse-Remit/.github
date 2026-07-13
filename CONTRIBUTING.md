# Contributing to PulseRemit

Thanks for wanting to contribute. PulseRemit is open infrastructure — every improvement makes cross-border payroll and remittance more accessible on Stellar. This guide applies as the default contribution process across all five repositories in this organization (`pulse-remit-contracts`, `pulse-remit-backend`, `pulse-remit-frontend`, `pulse-remit-docs`, and this `.github` repo).

## Before You Start

1. Read the [`.github` hub README](https://github.com/YOUR_ORG/.github) to understand how the five repositories relate to one another.
2. Identify which repository your change belongs in. Most changes touch exactly one repo — see the table below.
3. Check that repo's open issues for something already scoped, or open a new issue describing what you want to change before writing code for anything non-trivial.

| I want to... | Repository |
|---|---|
| Fix or extend a Soroban contract | `pulse-remit-contracts` |
| Change an API endpoint, add a SEP surface, fix backend logic | `pulse-remit-backend` |
| Fix a UI bug, add a page, improve accessibility | `pulse-remit-frontend` |
| Fix documentation, add a diagram, write a guide | `pulse-remit-docs` |
| Change contribution process, security policy, or issue templates | `.github` (this repo) |

## Workflow

1. Fork the specific repository you're changing.
2. Create a branch: `git checkout -b feat/your-feature`
3. Make your changes and add tests appropriate to that repo (see Code Standards below).
4. Run that repository's test suite locally — see its own README for exact commands.
5. Submit a PR against that repository's `develop` branch (or `main` if `develop` doesn't exist), using the PR template.
6. Link the issue your PR resolves.

## Code Standards by Repository

### `pulse-remit-contracts` (Rust / Soroban)
- `cargo fmt` and `cargo clippy -- -D warnings` must pass with zero warnings
- Every new public contract function requires at least one unit test covering the happy path and, separately, its expected error case
- Use `panic_with_error!(&env, ErrorType::Variant)` for contract errors — never a bare `panic!()`

### `pulse-remit-backend` (TypeScript / Express)
- Every new request body or query parameter must be validated with a Zod schema in `src/schemas/`, applied via `validateBody` / `validateParams` / `validateQuery`
- Every new endpoint needs at least a happy-path test in `src/__tests__/`
- Run `npm run build` (TypeScript compilation) and `npm test` before opening a PR

### `pulse-remit-frontend` (TypeScript / Next.js)
- Run `npm run type-check` and `npm run lint` before opening a PR
- New shared types belong in `types/index.ts`, not inlined in component files
- Prefer TanStack Query for all data fetching — avoid hand-rolled `useEffect` fetch chains

### `pulse-remit-docs` (Markdown)
- New Mermaid diagrams should follow the color conventions already established in existing docs (see `architecture/system-overview.md` for the palette)
- Run a local link check before submitting if you've added internal cross-references

## Commit Convention

`<type>(<scope>): <message>`

Example: `feat(payroll_vault): add advance request cap`

Types: `feat`, `fix`, `test`, `docs`, `chore`, `refactor`, `perf`, `security`

## Community Programs

Some issues across these repositories are labeled for participation in external open-source contributor and grant programs relevant to the Stellar ecosystem. Where that applies, it will be noted directly on the issue with the relevant label and any reward information. Absence of such a label does not mean a contribution isn't welcome or valuable — it simply means no external program is currently tracking that specific issue.

## Questions

For anything that spans more than one repository, open a Discussion in this `.github` repository rather than an issue in an individual repo.
