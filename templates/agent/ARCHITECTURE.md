# ARCHITECTURE.md — [Project Name]

> Structured for grepping, not reading. One fact per line where possible.

---

## System type

[e.g. Monolith / Microservices / Monorepo / Single-page app + API / etc.]

## Entry points

| Entry point | File | Purpose |
|---|---|---|
| HTTP API | | |
| Background jobs | | |
| CLI | | |
| Cron | | |

## Component map

```
[Component A] ── HTTP ──► [Component B]
      │
      ▼ (async, Redis queue)
[Worker]
      │
      ▼
[External: Stripe API]
```

## Module ownership

| Directory | Owns | Must not | Notes |
|---|---|---|---|
| `src/auth/` | Authentication, session management | Log passwords or tokens | |
| `src/billing/` | Payment flows, invoice generation | Touch user data directly | |
| `src/api/` | Route definitions, request validation | Business logic | |

## Data flow

[Where data enters, how it moves through the system, where it lands. Plain language.]

## External dependencies

| Service | What it does | Direction | Required / Optional |
|---|---|---|---|
| | | Inbound / Outbound / Both | |

## Database

| Table / Collection | Owns | Primary key | Notes |
|---|---|---|---|
| | | | |
