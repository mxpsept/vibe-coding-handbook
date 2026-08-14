# FlowOps — Security, Observability & Deployment Baseline

## Security
HTTPS; externalized secrets; server-side authorization; input validation; dependency vulnerability process; auth-appropriate CORS/CSRF; privileged-action audit; least-privilege credentials. Real production deployment requires threat modeling.

## Observability
Structured logs, correlation/trace id, latency/error metrics, dependency health, health/readiness endpoints, and separate business audit evidence.

## Deployment
`Reverse Proxy/Ingress → Frontend + /api Backend → Relational DB`. Environments: local, test, staging/UAT, production. Build versioned artifacts; version migrations; verify health; define rollback/roll-forward.

Redis, MQ, Elasticsearch, object storage and notification services are added only when an approved Driver requires them.