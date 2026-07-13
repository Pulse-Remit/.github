# 📘 Add OpenAPI 3.1 specification for the REST API

**Labels**: `documentation`, `backend`, `enhancement`, `help wanted`
**Complexity**: 🟡 Medium — API documentation experience helpful

## Summary
PulseRemit's REST API has 15+ endpoints across 4 route groups but no machine-readable API specification. Adding an OpenAPI 3.1 spec enables auto-generated client SDKs, makes the API self-documenting in Swagger UI, and makes it easy for new contributors to understand what they're building against.

## What needs to be done

1. Create `backend/openapi.yaml` (OpenAPI 3.1 format)
2. Cover all endpoints:
   - `GET/POST /api/v1/employees` and sub-routes
   - `GET/POST /api/v1/remittances` and sub-routes
   - `GET/PATCH/POST /api/v1/vault`
   - `GET/POST /api/v1/compliance`
   - `GET /sep31/info`, `POST /sep31/transactions`, `GET/PATCH /sep31/transactions/:id`
   - `GET /sep38/info`, `GET /sep38/prices`, `POST/GET /sep38/quote`
   - `GET/POST /auth`
3. Wire Swagger UI: add `swagger-ui-express` to serve at `GET /api-docs`
4. All request/response schemas must match the existing Zod validators

## Acceptance criteria
- [ ] `openapi.yaml` covers all endpoints with request/response schemas
- [ ] `GET /api-docs` serves interactive Swagger UI
- [ ] At least one request/response example per endpoint
- [ ] Zod schema names match OpenAPI component names

## Stellar Wave
Points: 100 | Complexity: 🟡 Medium
