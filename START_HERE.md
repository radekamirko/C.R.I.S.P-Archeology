# START HERE — CRISP Archaeology

You have a codebase. You have no docs. You need to figure out what you inherited before you touch anything.

This is CRISP Archaeology. It reads the code, builds a strawman, asks you to correct it, and produces a full doc set — for humans and for Claude Code.

---

## Setup

**Option A — Run Archaeology on an existing project (recommended)**

Clone Archaeology into your existing project folder:

```bash
cd my-existing-project
git clone https://github.com/radekamirko/C.R.I.S.P-Archeology .crisp-archaeology
claude
```

Your project stays untouched. Archaeology lives in `.crisp-archaeology/`. Outputs go to `docs/` in your project root.

**Option B — Standalone**

```bash
git clone https://github.com/radekamirko/C.R.I.S.P-Archeology
cd C.R.I.S.P-Archeology
claude
```

---

## Start

Once Claude is running:

**With slash commands:**
```
/crisp-archaeology
```

**Any Claude (no slash commands):**
```
Read .crisp-archaeology/.claude/skills/crisp-archaeology/SKILL.md and run CRISP Archaeology on this repo.
```

Claude will ask one question — whether to include git history — then get to work.

---

## What happens

| Step | What Claude does |
|---|---|
| **Recon** | Reads the repo silently — git log, manifests, entry points, CI, tests, folder structure |
| **Strawman** | Presents a deliberately incomplete skeleton for you to correct |
| **Elicitation** | Resolves every gap — presents assumptions, never commits without your confirmation |
| **Output** | Full `docs/` folder + agent-ready context files |

---

## What you get

**`docs/`** — for humans  
System Overview, Architecture Map, Tech Stack, Domain Glossary, Business Context, Risk Register, Feature Inventory, Decision Log, Open Questions, Runbook Skeleton

**Repo root** — for Claude Code  
`CLAUDE.md`, `ARCHITECTURE.md`, `SECURITY.md`, `DEPLOYMENT.md`, `CONVENTIONS.md`, per-directory `CLAUDE.md` files

---

## After Archaeology

Your project is in the same state as one that completed CRISP Phase I.

Hand it off to [CRISP](https://github.com/radekamirko/C.R.I.S.P) Phase S or drop straight into a Sprint.

---

*"Your codebase is the brief."*
