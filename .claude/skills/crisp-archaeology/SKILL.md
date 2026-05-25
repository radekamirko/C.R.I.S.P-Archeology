# CRISP Archaeology — SKILL.md

**Version:** 1.0  
**Entry point:** User says "run archaeology on [path]" or "start CRISP Archaeology"

---

## What this skill does

Reverse-engineers an existing codebase into two output sets:

1. **Human artifacts** — discovery docs for stakeholders, consultants, and future developers
2. **Agent-ready docs** — durable context files for Claude Code (CLAUDE.md, SECURITY.md, etc.)

The process runs across multiple turns. It never assumes. It presents inferences for confirmation. It only commits facts that are unambiguous in code.

---

## Phases

### Phase 1 — Solo Recon (no user input required)

**Goal:** Walk into Phase 2 with sharp, specific inferences — not a blank slate, not wrong guesses you've hidden.

Read the repo in this order:

1. **README** — read it, note what it _claims_, flag it as unverified
2. **Git log — contributors**
   ```
   git log --all --pretty=format:"%an" | sort | uniq -c | sort -rn
   ```
   Note: top committers, how concentrated authorship is, whether the primary author is still around
3. **Git log — commit cadence**
   ```
   git log --pretty=format:"%ad" --date=short | sort | uniq -c
   ```
   Note: lifecycle shape — ramp-up, plateau, abandonment, revival?
4. **Last 50 commit messages** — current vocabulary, what's broken, what's changing
5. **Last 10 closed PRs** (if GitHub) — same signal, richer context
6. **Dependency manifests** — `package.json`, `requirements.txt`, `go.mod`, `Gemfile`, `pom.xml`, etc. This is ground truth for tech stack, not the README
7. **Entry points** — `main.py`, `index.ts`, `Dockerfile CMD`, `start` script. Trace 2 levels outward only. Do not read the whole codebase
8. **Folder structure** — read as an org chart. Folders map to bounded contexts or teams
9. **CI/CD config** — `.github/workflows`, `.gitlab-ci.yml`, etc. Surfaces deployment story, environments, test maturity
10. **Issue/PR labels** (if GitHub) — product taxonomy, business domains
11. **Test files** (skim, not source) — describe intent. `test_invoice_generation.py` > reading the invoice module
12. **Existing docs** — treat as unverified. Note what they claim, flag for confirmation

**After recon, produce:**
- A draft strawman (see Phase 2)
- A list of ✅ hard facts (directly confirmed from code/config with no interpretation needed)
- A list of ❓ inferences (pattern-matching that needs confirmation)
- A list of ❌ unknowns (business context that code cannot reveal)

**✅ rule:** Only mark as ✅ if it would be obvious to any developer reading that file. When in doubt, mark ❓.

Examples:
- `"uses Node 18"` from package.json engines field → ✅
- `"this is a multi-tenant SaaS"` from seeing a tenant_id column → ❓ (confirm)
- `"why this was built"` → ❌ always

---

### Phase 2 — Strawman

**Goal:** Present a deliberately incomplete, probably-wrong-in-places skeleton. The human corrects it. This is 5x faster than asking open-ended questions.

Present the strawman in this structure:

```
## What I think this system does
[one paragraph, business terms only]
"I'm assuming this is [X] for [Y]. Correct me."

## Who I think uses it
[roles identified from auth/permissions code]
"I see roles: admin, user, [X]. Are these right? Anyone missing?"

## Architecture as I understand it
[boxes and arrows in plain text or ASCII]
"I've put a ❓ on [specific arrows I'm unsure about]"

## Tech stack (confirmed from manifests)
[table — only ✅ items here]

## Integrations I can see
[third-party services found in code/config]
"I can see calls to [Stripe / Twilio / etc.]. Are there others not visible in the repo?"

## What I can't figure out from code alone
[named unknowns — specific, not vague]
"I see a `worker/` directory with Redis. I'm assuming background jobs. What jobs?"
"There's a `billing/` module. I don't know the pricing model."
```

After presenting, say:
> "Correct what's wrong. Confirm what's right. Skip what you don't know — I'll mark it as an open question."

---

### Phase 3 — Elicitation

**Goal:** Resolve every ❓ and fill every ❌ that the human can answer. Park the rest as open questions.

Rules:
- Never ask open-ended "what does this do?" — always ask specific, answerable questions
- Batch by artifact — all business context questions together, all architecture questions together
- If you can detect a pattern and make an assumption, present it: "I'm assuming X — is that right?" 
- If the human doesn't know, mark it as `🔓 Open — needs [owner]`
- Never save an assumption as truth without explicit confirmation
- Maximum ~5 questions per turn — don't interrogate

After each answer:
- If confirmed → mark ✅, write it to the relevant artifact draft
- If corrected → update and note what changed
- If unknown → mark 🔓, note who might know

Continue until no ❓ remain (all are either ✅ or 🔓).

---

### Phase 4 — Output Generation

**Goal:** Produce both output sets.

#### Human artifacts → `docs/`

| File | What it is |
|---|---|
| `docs/system-overview.md` | 1-page max. Business terms. What it does, who uses it, what breaks if it dies. |
| `docs/architecture-map.md` | Boxes and arrows (text). One paragraph per component: responsibility + what breaks if it dies. Includes external deps. |
| `docs/tech-stack.md` | Table: component, language, framework, version, hosting, owner, criticality, last-touched. |
| `docs/domain-glossary.md` | Every domain term with one-line definition + where it lives in code. |
| `docs/business-context.md` | Prose, 1–2 pages. Who pays, why, value exchange, competitive context, "worst bug we could ship." |
| `docs/risk-register.md` | Two columns: known risks (debt, SPOFs, key-person deps, version EOLs) + known constraints (regulatory, lock-in, historical decisions). |
| `docs/feature-inventory.md` | Table: feature, entry point, status (implemented/stub/broken), notes. Recovered from routes/controllers. |
| `docs/decisions.md` | Running log: "We chose X over Y because Z." Start with what recon and elicitation revealed. |
| `docs/open-questions.md` | Everything unresolved. Owner + priority. Honesty as an artifact. |
| `docs/runbook-skeleton.md` | Structure only if not fully known: deploy, rollback, logs location, failure modes, who to call. |

#### Agent-ready docs → repo root + per-directory

| File | What it is |
|---|---|
| `CLAUDE.md` | Root orientation. What this is, what matters, conventions, what never to touch, how to run tests, how to commit. Dense, declarative, imperative. |
| `ARCHITECTURE.md` | Text version of the architecture map. Structured for grepping, not reading. |
| `SECURITY.md` | Auth model, PII boundaries, secrets handling, things-the-agent-must-never-do. Rules, not policy. |
| `DEPLOYMENT.md` | Environments, deploy commands, rollback, env vars, infra. Operational, not architectural. |
| `CONVENTIONS.md` | Naming, file layout, error handling, testing patterns, unwritten rules. Prevents foreign-looking code. |
| `GLOSSARY.md` | Same as domain glossary — standalone so it can be linked from CLAUDE.md. |
| `[dir]/CLAUDE.md` | Per-directory context. What this module owns, what it must never do, special rules. Generate for every top-level module/service directory. |

#### After generation:
- Write `crisp-state.json` marking Archaeology as complete, entry point set to Phase S or Sprint
- Present the output summary to the user

---

## Confidence rules

| Signal | Classification |
|---|---|
| Explicitly in config/manifest with no interpretation | ✅ Hard fact |
| Pattern-matched from code, plausible but interpretive | ❓ Confirm |
| Business context, intent, history, future direction | ❌ Cannot recover — elicit |
| Human confirmed during elicitation | ✅ Confirmed |
| Human doesn't know | 🔓 Open question |

---

## What code can tell you (start ✅)

- Tech stack — languages, frameworks, library versions from manifests
- Data model — entities, relationships, fields from schema/migrations
- Feature inventory — routes, controllers, API endpoints
- Integrations — third-party API calls, webhook configs, env var names (not values)
- Auth patterns — roles, permission checks, JWT vs session
- Deployment — Dockerfile, CI config, environment names
- Commit history — who wrote it, when, what the current vocabulary is
- Test intent — what behaviors were spec'd (from test file names and descriptions)

## What code cannot tell you (always ❌)

- Why it was built
- Who it's really for (beyond role names in code)
- Business model and value exchange
- Market context and competitors
- What "success" looks like
- Stakeholder map
- Decisions that were rejected
- Regulatory or contractual constraints
- Future direction and roadmap intent

---

## Output quality bar

- System Overview: if it's longer than 1 page, it's not done yet
- CLAUDE.md: imperative and specific. "Use X. Never Y. When Z, do W." Not "we tend to prefer..."
- Per-directory CLAUDE.md: if a module has no special rules, still write one — at minimum: what it owns and where to find its tests
- Open Questions: never hide unknowns. A rigorous open questions log is a signal of quality work, not incompleteness
- Every artifact: named owner field + review date at top

---

## Starting the skill

When the user invokes Archaeology:

1. Ask for the repo path (local) if not provided
2. Confirm scope: "Should I include git history in the scan, or current state only?"
3. Run Phase 1 recon silently
4. Present the strawman (Phase 2)
5. Run elicitation turns (Phase 3)
6. Generate output (Phase 4)
7. Summarize what's ✅ complete, what's 🔓 open, and recommended next step (Phase S or Sprint)
