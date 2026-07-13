# REST API cursor-based pagination for remittances

**Complexity**: low

## Summary
`GET /api/v1/remittances` uses offset-based pagination. For large datasets this is inefficient. Implement cursor-based pagination using `createdAt` as the cursor.

## Acceptance criteria
- [ ] Add `cursor` query param (ISO timestamp string)
- [ ] Returns `nextCursor` in response
- [ ] Existing `page`/`limit` params remain for backwards compatibility
- [ ] Tests for cursor behavior (first page, next page, last page)

## Stellar Wave
Points: 100 | Complexity: 🟢 Low
