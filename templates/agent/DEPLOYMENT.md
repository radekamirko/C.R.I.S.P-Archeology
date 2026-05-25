# DEPLOYMENT.md — [Project Name]

> Operational, not architectural. How to ship and how to survive a bad ship.

---

## Environments

| Environment | URL | Branch | Deploy trigger |
|---|---|---|---|
| Production | | `main` | |
| Staging | | `staging` | |
| Local | `localhost:3000` | any | manual |

## Deploy process

```bash
# Standard deploy
[command or process]

# What happens during deploy (in order)
# 1. [build step]
# 2. [migration step]
# 3. [restart/swap step]
```

## Rollback

```bash
# How to roll back a bad deploy
[command or process]

# How to check if rollback was successful
[command]
```

## Environment variables

| Variable | Purpose | Required | Default |
|---|---|---|---|
| `DATABASE_URL` | Postgres connection string | Yes | — |
| `SECRET_KEY` | Session signing | Yes | — |

*Values live in: [.env / Secrets Manager / etc.]*  
*Never commit values to git.*

## Migrations

```bash
# Run migrations
[command]

# Rollback migration
[command]
```

**Migration rule:** [e.g. always backwards-compatible / zero-downtime required / etc.]

## Infrastructure

| Component | Provider | Region | Notes |
|---|---|---|---|
| App server | | | |
| Database | | | |
| Cache | | | |
| Object storage | | | |

## Health check

```
[URL or command to verify system is healthy after deploy]
```
