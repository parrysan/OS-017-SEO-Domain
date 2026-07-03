---
title: "OS-017 — SEO Domain"
type: project-bootstrap
created: "2026-07-03"
---

# OS-017 — SEO Domain

> **Bootstrap order — read these in order before doing any work in this project:**
>
> 1. `~/.claude/CLAUDE.md` → `Open-Memory-Vault/system/identity/MASTER-PROMPT.md` — Phil's identity (auto-loaded via symlink in Claude Code; other tools should mirror this).
> 2. `~/AGENT.md` → `agent-config/AGENT.md` — global operating manual (work style, skills routing, secrets policy, layering rules in §2.10).
> 3. `Open-Memory-Vault/AGENTS.md` — vault operating contract (read **only** if you will write to the vault during this session).
> 4. `Open-Memory-Vault/projects/OS-017-SEO-Domain/README.md` — durable project page (status, decisions, recent activity, vault-side context).
> 5. **This file (`CLAUDE.md`)** — project-specific overrides and live operational references (below).
>
> **The project's `CLAUDE.md` is a bootstrap manifest, not a knowledge dump.** It points at everything else. Durable knowledge lives in the vault project page. Do not duplicate.

---

## At a glance

- **Code**: `OS-017`
- **Name**: SEO Domain
- **Stakeholder**: Phil (self)
- **Type**: `aios`
- **Status**: `active`
- **Priority**: `medium`
- **Revenue lane**: `4-aios`
- **Autonomy mode**: `autopilot` — audits and monitoring cycles run end-to-end; Phil reviews at report and implementation-plan checkpoints.
- **Purpose** (one sentence): A reusable SEO operating environment inside the AIOS — deep audits, AI-search/GEO/AEO readiness, implementation planning, and reporting, dispatchable per website/property for Oganiko's clients.
- **Last touched**: `2026-07-03`

---

## Where things live

| Resource | Location |
|---|---|
| **Code root** | this folder (`dev/OS-017-SEO-Domain/`) |
| **Domain definition + architecture** | `./docs/seo-domain-design.md` |
| **Per-property engagements** | `./properties/<domain>/` (context, data, audits, plans, reports) |
| **Project docs** | `./docs/` |
| **Vault project page** | `Open-Memory-Vault/projects/OS-017-SEO-Domain/README.md` |
| **GitHub repo** | https://github.com/parrysan/OS-017-SEO-Domain |
| **External systems** | Google Search Console (per client, via `gws`), skills.sh registry |

---

## Live references

> **Operational facts that should never have to be re-discovered.** Update this section whenever a fact changes — it is the canonical source.

- **Production URL**: none — internal operating environment, not a deployed site
- **Skills registry**: https://skills.sh/ — search via `npx skills find <query>` (meta-find-skills skill)
- **Installed ecosystem skills**: see `./docs/seo-domain-design.md` §Toolkit
- **Credentials**: none stored here — GSC/analytics access via `gws` OAuth; client API keys in global `.env`

---

## Tech stack

Markdown-first operating environment — skills, agents, templates, and per-property data folders. No web stack. Python 3 stdlib for any crawl/parse scripts (zero-dependency convention, as OS-009).

---

## Project-specific rules

- **Client data is private.** `properties/` is gitignored — per-client crawl data, GSC exports, and reports never land in the public repo. Only the environment (skills, templates, docs) is versioned publicly.
- **Outputs must be actionable.** Every audit finding carries: evidence, impact/effort score, owner domain (content/design/dev), and a concrete fix. No generic advice.
- **One engagement = one folder** under `properties/<domain>/` created from `templates/property/`.

---

## Skills

- **Project-local skills**: none yet — environment skills live in the global library (see design doc §Toolkit)
- **Most relevant global skills for this project**: `meta-find-skills`, `marketing:seo-audit`, `audit-website`, `deep-research`, `research`, `og-deploy`

---

## Notes for the next session

Last action: initial scaffold + SEO domain design (docs/seo-domain-design.md). Next action: install chosen ecosystem skills, run first pilot audit on a real property. Open question: which property is the pilot (steveapps.co? tartak?).
