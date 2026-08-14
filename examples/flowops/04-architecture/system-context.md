# FlowOps — System Context v0.1

## System of Interest

```text
FlowOps
Enterprise Supervision & Execution Tracking System
```

## Actors

```text
Responsible Participant
Supervision Specialist
Department Manager
Manager
Closure Authority (exact mapping pending)
Administrator
```

## Context Diagram

```text
                   ┌───────────────────────┐
                   │ Organization / SSO    │
                   │ future/optional       │
                   └──────────┬────────────┘
                              │ identity/org
                              ▼
┌────────────────┐      ┌─────────────────────────┐
│ Enterprise User│─────▶│                         │
└────────────────┘ HTTPS│         FlowOps         │
                        │                         │
┌────────────────┐      │ supervision lifecycle  │
│ Manager        │─────▶│ progress / attention   │
└────────────────┘      │ closure / audit         │
                        └──────────┬──────────────┘
                                   │ future notifications
                                   ▼
                        ┌─────────────────────────┐
                        │ Notification Provider   │
                        │ future/optional         │
                        └─────────────────────────┘
```

## In Scope — MVP Core

FlowOps owns:
- supervision item lifecycle；
- accountability/deadline facts；
- progress history；
- attention semantics/query；
- completion claim / closure；
- application-level audit evidence；
- role/scope enforcement based on identity information available to it。

## Out of Scope / External Candidate

```text
HR master data
enterprise identity provider
SMS/email/IM delivery infrastructure
enterprise document platform
BI platform
```

If these are integrated later, FlowOps consumes explicit contracts rather than duplicating entire external domains.

## Trust Boundaries

```text
Browser
  │ untrusted client
  ▼
Backend API
  │ trusted application boundary
  ▼
Database / controlled infrastructure
```

Frontend data/actions are never trusted for authorization or lifecycle transition correctness.

External integrations form separate trust boundaries and require authentication, timeout, failure handling and observability.

## Context Questions

Before production architecture:
- What is the enterprise identity provider?
- Is organization hierarchy authoritative outside FlowOps?
- Are attachments stored by FlowOps or an external document service?
- What notification providers are mandatory?
- Is FlowOps internet-facing, intranet-only or hybrid?
- What audit retention/compliance requirements apply?

Unknown answers remain architecture gaps, not implementation guesses.
