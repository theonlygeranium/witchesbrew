# [PROJECT NAME] — Agent Continuity Brief
**Last updated:** YYYY-MM-DD by [agent/session id]
**Purpose:** Drop-in context document for any new WRITER Agent or Codex session working on this project. Read this before touching anything.

---

## Project Identity
- **Project name:** [PROJECT NAME]
- **Owner:** EdStratum Labs (`founder@edstratumlabs.ai`)
- **Live URL:** `https://[your-domain]`
- **Repo:** `https://github.com/theonlygeranium/[witchesbrew]` (private/public)
- **Default branch:** `main` → auto-deploys to Schubert on push

---

## Stack
| Layer | Technology |
|-------|-----------|
| <!-- e.g. Frontend --> | <!-- e.g. Next.js 15 --> |
| <!-- e.g. Backend --> | <!-- e.g. FastAPI --> |
| <!-- e.g. Database --> | <!-- e.g. PostgreSQL 18 --> |
| CI/CD | GitHub Actions → Schubert self-hosted runner |
| Deploy target | Schubert Nexus at `/opt/[witchesbrew]/` |

---

## Repository Key Files
```
[witchesbrew]/
├── AGENTS.md               ← Agent rules — read first
├── CONTINUITY_BRIEF.md     ← This file — update after every session
├── README.md               ← Human-readable overview
├── CHANGELOG.md            ← All changes — updated every commit
├── REVERT.md               ← Stable baseline + rollback instructions
├── .env.example            ← Non-secret env var template
├── scripts/deploy.sh       ← Called by GitHub Actions
└── docs/
    ├── architecture.md     ← Current system design
    ├── setup.md            ← Local dev + Schubert deploy guide
    ├── decisions/          ← ADRs
    └── runbooks/           ← Operational runbooks
```

---

## CI/CD Pipeline
- Push to `main` → `schubert-local` self-hosted runner picks up job → runs `scripts/deploy.sh` directly on Schubert
- Remote fallback: `workflow_dispatch → force_remote: true` → Tailscale OAuth → SSH to Schubert
- Required secrets: `SCHUBERT_SSH_KEY`, `TS_OAUTH_CLIENT_ID`, `TS_OAUTH_SECRET` (pre-provisioned on all repos)

---

## Current State
<!-- TODO: Fill in after initial project setup -->
- **Last stable tag:** `v0.1-stable` → commit `[SHA]`
- **Active branch:** `main`
- **Open work:** [describe any in-flight features or known issues]
- **Services on Schubert:** [list systemd services this project uses]

---

## Environment Variables
<!-- List all required env vars. See .env.example for full list. -->
| Variable | Description | Where Set |
|----------|-------------|-----------|
| `EXAMPLE_VAR` | Description | Schubert `/opt/[witchesbrew]/.env` |

---

## Credentials Reference
| Secret | Location | Note |
|--------|----------|------|
| Schubert SSH key | GitHub Secret `SCHUBERT_SSH_KEY` | Pre-provisioned |
| Tailscale OAuth | GitHub Secrets `TS_OAUTH_CLIENT_ID` + `TS_OAUTH_SECRET` | Pre-provisioned |

---

## Rules Every Agent Must Follow
1. Update this file at the end of every session with current state.
2. Never commit secrets to source — all keys go in Schubert `.env` or GitHub Secrets.
3. Update `CHANGELOG.md` on every commit.
4. Create an ADR in `docs/decisions/` for every architectural decision.
5. Query Schubert live state before making assumptions about running services.
6. See `AGENTS.md` for full rules.
