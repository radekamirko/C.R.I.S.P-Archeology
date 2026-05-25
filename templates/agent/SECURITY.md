# SECURITY.md — [Project Name]

> Rules, not policy. These are hard constraints for any agent working in this repo.

---

## Auth model

[How authentication works. JWT? Sessions? OAuth? Who issues tokens?]

## PII and sensitive data

| Data type | Where it lives | Classification | Rules |
|---|---|---|---|
| Email addresses | | PII | Never log |
| Payment data | | PCI | Never store raw — use Stripe token only |
| Passwords | | Secret | Hashed with bcrypt, never log, never return in API response |

## What you must never do

- Never log: [list — e.g. passwords, tokens, card numbers, raw PII]
- Never return in API responses: [list]
- Never commit to git: [list — e.g. .env files, private keys, credentials]
- Never skip: [e.g. input validation on user-supplied data]

## Secrets handling

- Secrets live in: [.env / AWS Secrets Manager / Vault / etc.]
- Pattern for accessing secrets: [how the codebase reads them]
- Never hardcode secrets. If you see one hardcoded, flag it immediately.

## Threat model (summary)

[What are the realistic attack vectors for this system? What data is most at risk?]

## Compliance requirements

[GDPR / HIPAA / PCI / SOC2 / none — and what that means practically for this codebase]
