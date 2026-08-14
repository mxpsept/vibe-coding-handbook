# FlowOps — API Contract v0.1

## Principles
Domain actions over arbitrary field mutation; consistent errors; server authorization; one pagination/filter convention; OpenAPI is the executable-contract candidate.

## Queries
`GET /api/items`, `/api/items/{id}`, `/api/my-work`, `/api/attention`, `/api/management-review`.

## Commands
`POST /api/items`, `/items/{id}/progress-updates`, `/items/{id}/completion-claims`, `/items/{id}/closure`.

Avoid generic `PUT /items/{id} {status:CLOSED}` because it hides lifecycle rules.

Lifecycle-changing commands should detect stale versions and return `409 Conflict` with a stable machine code. Prefer additive contract evolution; frontend must not depend on undocumented fields.