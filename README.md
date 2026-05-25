# CRISP Archaeology

**Reverse-engineer a codebase into a full CRISP project skeleton.**

> *"Your codebase is the brief."*

A companion to [CRISP](https://github.com/radekamirko/C.R.I.S.P) — the open-source framework for scoping and speccing AI projects. Archaeology is the entry point for projects that already have code but no docs.

---

## → [START HERE](./START_HERE.md)

---

## The problem

Most real-world projects have code but no discovery artifacts. Inherited repos, dev handovers, agencies picking up mid-project, founders who built fast and now need to plan the next phase properly. Running CRISP from scratch on an existing project is wasteful — half the work is already encoded in the code.

CRISP Archaeology reads the codebase and recovers what it can. Then it asks targeted questions for the rest.

---

## What it produces

### Human artifacts (`docs/`)
For stakeholders, consultants, and future developers:
- **System Overview** — what it does, who uses it, what breaks if it dies
- **Architecture Map** — components, responsibilities, external dependencies
- **Tech Stack Inventory** — ground truth from manifests, not the README
- **Domain Glossary** — the private language of the codebase, defined
- **Business Context Memo** — who pays, why, what matters most
- **Risk & Constraint Register** — technical debt, SPOFs, known constraints, the graveyard
- **Feature Inventory** — every route, endpoint, and feature with its current status
- **Decision Log** — why things are the way they are
- **Open Questions Log** — everything that couldn't be recovered, with owners
- **Runbook Skeleton** — deploy, rollback, failure modes

### Agent-ready docs (repo root)
For Claude Code and other LLM coding agents:
- `CLAUDE.md` — orientation, conventions, what never to touch
- `ARCHITECTURE.md` — structured for grepping, not reading
- `SECURITY.md` — auth model, PII rules, hard constraints
- `DEPLOYMENT.md` — environments, deploy commands, rollback
- `CONVENTIONS.md` — naming, error handling, testing patterns, unwritten rules
- Per-directory `CLAUDE.md` — local context for every module

---

## How it works

Four phases across multiple conversation turns:

1. **Solo recon** — Claude reads the repo (git log, manifests, entry points, CI config, tests, folder structure) without asking a single question
2. **Strawman** — Claude presents a deliberately incomplete skeleton. You correct it. Much faster than Q&A.
3. **Elicitation** — Claude resolves every gap. Presents assumptions for confirmation. Never saves anything as truth without your sign-off. Parks what you don't know as open questions.
4. **Output** — Full `docs/` folder + agent-ready context files

After Archaeology completes, the project is in the same state as a project that completed CRISP Phase I. Phase S or Sprint sessions pick up from there.

---

## Confidence model

| Marker | Meaning |
|---|---|
| ✅ | Confirmed from code or by you |
| ❓ | Inferred — needs confirmation |
| ❌ | Cannot recover from code — needs human |
| 🔓 | Open question — nobody could answer it yet |

---

## Part of the CRISP ecosystem

```
Standard CRISP:    Phase R → Phase I → Phase S → Sprints
CRISP Archaeology: Scan → Elicitation → docs/ → Phase S or Sprints
```

- [CRISP](https://github.com/radekamirko/C.R.I.S.P) — the main framework
- CRISP Archaeology (this repo) — entry point for existing codebases

---

## Built by Mileva

CRISP Archaeology is part of the CRISP open-source ecosystem, built by [Mileva](https://mileva.io) — an AI automation agency that builds workflow systems replacing entire operational teams.

**Questions, PRs, or war stories from the field:** open an issue or find me on [X @radekamirko](https://x.com/radekamirko).

---

## Status

🚧 v1.0 — skill and templates complete, not yet battle-tested on a real repo.

---

*Outcome first. Always.*
