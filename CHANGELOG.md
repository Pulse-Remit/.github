# Changelog

This changelog tracks the project at the **organizational level**: which
versions of `pulse-remit-contracts`, `pulse-remit-backend`, and
`pulse-remit-frontend` are known to work together, and major structural
changes to the project as a whole (such as the repository split described
below). For implementation-level changes within a single repository, see
that repository's own `CHANGELOG.md`.

## [Unreleased]

### Changed — Repository restructuring

The project was restructured from a single monorepo into five independent
repositories: `pulse-remit-contracts`, `pulse-remit-backend`,
`pulse-remit-frontend`, `pulse-remit-docs`, and this `.github` governance
repository. See the [hub README](./README.md#3-repository-constellation)
for the full rationale.

As part of this restructuring:
- Backend Zod validation schemas were extracted from inline route
  definitions into a dedicated `src/schemas/` module for reuse and clarity
- A `src/types/`, `src/constants/`, and `src/utils/` layer was added to
  the backend for shared type definitions and protocol-level constants
  (fee caps, corridor lists, FX rates) that were previously duplicated
  inline across controllers
- `validateQuery` middleware was added to the backend's validation layer
  for consistency with the existing `validateBody` / `validateParams`
  (previously, query-parameter routes like SEP-10's challenge endpoint
  validated manually with ad-hoc `if` checks)
- **Fixed a critical frontend build defect**: `tsconfig.json`'s `@/*` path
  alias pointed at a `./src/*` directory that does not exist in this
  project's flat (non-`src`) folder structure, meaning every `@/`-prefixed
  import across the entire frontend — roughly a dozen files — would have
  failed to resolve at build time. Corrected to `./*`
- A real `useWallet()` hook (`hooks/useWallet.ts`) was implemented for
  Freighter wallet connection and transaction signing, replacing the
  previously non-functional static "Connect Freighter" button
- Fixed a stale Docker Compose build context: `docker-compose.yml`'s
  backend service pointed at a `./backend` build context left over from
  the monorepo layout; corrected to `.` now that the file lives inside
  the backend repository directly
- Per-repository CI workflows replace the single monorepo-wide workflow,
  so a contracts-only change no longer triggers a frontend build and
  vice versa

### Version Compatibility Matrix

| `pulse-remit-contracts` | `pulse-remit-backend` | `pulse-remit-frontend` | Status |
|---|---|---|---|
| `0.1.0` | `0.1.0` | `0.1.0` | Current — SEP-31/38/10 compliant, five-repo structure |

## [0.0.1] — Pre-split monorepo baseline

- `PayrollVault` Soroban contract: fund, schedule, claim, advance
- `RemittanceRouter` Soroban contract: cross-border payments with fee collection
- `ComplianceRegistry` Soroban contract: on-chain KYC/AML verdict store
- `StableSwap` Soroban contract: corridor FX liquidity pool
- Express REST API with full CRUD for employees, remittances, vault, compliance
- SEP-1, SEP-10, SEP-31, SEP-38 backend surfaces
- Stellar event indexer with PostgreSQL persistence
- Next.js 14 frontend: dashboard, send flow, compliance lookup
- Docker Compose dev stack (PostgreSQL + Stellar sandbox)
