# FlowOps — Error Model v0.1

Categories: `VALIDATION`, `BUSINESS_RULE`, `UNAUTHORIZED`, `FORBIDDEN`, `NOT_FOUND`, `CONFLICT`, `INFRASTRUCTURE`, `INTERNAL`.

User-relevant errors expose a stable machine code, safe human message, trace/correlation id, and safe details where useful. Do not normalize everything to HTTP 200 or leak stack traces/SQL/secrets.

UX mapping: 401 authentication flow; 403 permission explanation; 409 refresh/reconcile; business validation in action context; infrastructure failure with retry/support + traceId.

Coding Agents reuse the central error model instead of feature-specific envelopes or generic `RuntimeException("操作失败")`.