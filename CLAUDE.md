---
title: "OS-000-SEO — SEO/AEO Skill Centre"
type: project-bootstrap
created: "2026-07-03"
---

# OS-000-SEO — SEO/AEO Skill Centre

> **Bootstrap order — read these in order before doing any work in this project:**
>
> 1. `~/.claude/CLAUDE.md` → `Open-Memory-Vault/system/identity/MASTER-PROMPT.md` — Phil's identity (auto-loaded via symlink in Claude Code; other tools should mirror this).
> 2. `~/AGENT.md` → `agent-config/AGENT.md` — global operating manual (work style, skills routing, secrets policy, layering rules in §2.10).
> 3. `Open-Memory-Vault/AGENTS.md` — vault operating contract (read **only** if you will write to the vault during this session).
> 4. `Open-Memory-Vault/projects/OS-000-SEO/README.md` — durable project page (status, decisions, recent activity, vault-side context).
> 5. **This file (`CLAUDE.md`)** — project-specific overrides and live operational references (below).
>
> **The project's `CLAUDE.md` is a bootstrap manifest, not a knowledge dump.** It points at everything else. Durable knowledge lives in the vault project page. Do not duplicate.

---

## At a glance

- **Code**: `OS-000`
- **Name**: SEO — SEO/AEO Skill Centre
- **Stakeholder**: Phil (self)
- **Type**: `aios`
- **Status**: `active`
- **Priority**: `medium`
- **Revenue lane**: `4-aios`
- **Autonomy mode**: `autopilot` — audits and monitoring cycles run end-to-end; Phil reviews at report and implementation-plan checkpoints.
- **Skill centre**: `SEO/AEO` (code `seo`)
- **Purpose** (one sentence): The **SEO/AEO Skill Centre** — the AIOS centre of excellence for organic findability: deep audits, AI-search/GEO/AEO readiness, implementation planning, and reporting, dispatchable per website/property for Oganiko's clients. Reference implementation of the skill-centre pattern (`~/OG/ai-os/skill-centres.md`).
- **Last touched**: `2026-07-09` — full skill-registration audit: added `site-architecture`, registered `audit-website` (the crawl engine `squirrel` already referenced by name), added sxo-agent + e-commerce/multilingual/drift dispatch triggers

---

## Where things live

| Resource | Location |
|---|---|
| **Code root** | this folder (`dev/OS-000-SEO/`) |
| **Domain definition + architecture** | `./docs/seo-domain-design.md` |
| **Per-property engagements** | `./properties/<domain>/` (context, data, audits, plans, reports) |
| **Project docs** | `./docs/` |
| **Vault project page** | `Open-Memory-Vault/projects/OS-000-SEO/README.md` |
| **GitHub repo** | https://github.com/parrysan/OS-000-SEO |
| **Research store** | [OG-Research/OS-000-SEO](https://drive.google.com/drive/folders/1madR_jsEKKdni9R_E_3geGk0by_GrAb5) (`research/`, `assets/`, `deliverables/`) |
| **External systems** | Google Search Console (per client, via `gws`), skills.sh registry |

---

## Live references

> **Operational facts that should never have to be re-discovered.** Update this section whenever a fact changes — it is the canonical source.

- **Production URL**: none — internal operating environment, not a deployed site
- **Skills registry**: https://skills.sh/ — search via `npx skills find <query>` (meta-find-skills skill)
- **Audit engine**: claude-seo plugin (`claude-seo@agricidaniel-claude-seo`, user scope) — `/seo audit|page|schema|geo|content|local|backlinks|drift`
- **Installed ecosystem skills**: `seo-audit`, `ai-seo`, `programmatic-seo`, `site-architecture`, `seo`, `audit-website` (squirrelscan crawl engine) in `~/.agents/skills/` — full toolkit in `./docs/seo-domain-design.md` §Toolkit
- **Credentials**: none stored here — claude-seo Google creds in `~/.config/claude-seo/` (per-client OAuth at kickoff); client API keys in global `.env`

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

- **Front-door skill**: `og-seo-health-check` (global library) — domain URL → scored SEO/AEO readiness report against this centre's domain law
- **Intelligence loop**: `docs/intelligence/` — seo-scout-spec.md (weekly Hermes cron, pending install) + notebooklm-standing-prompt.md (monthly LAW CHECK report); pattern generalized in `~/OG/ai-os/skill-centres.md` §Intelligence loop
- **Project-local skills**: none — environment skills live in the global library (see design doc §Toolkit)
- **Ecosystem skills** (installed globally, dispatched per design doc §3/§4): `seo-audit`, `ai-seo`, `programmatic-seo`, `site-architecture`, `seo` (addyosmani/web-quality-skills), `audit-website` (squirrelscan — the crawl engine `squirrel` referenced throughout §3/§4)
- **claude-seo plugin specialists** (`/seo` commands + Agent-tool subagents, 25 skills/18 agents incl. `seo-sxo`, `seo-ecommerce`, `seo-hreflang`, `seo-drift` added 2026-07-09): full dispatch-profile table is `docs/seo-domain-design.md` §3, not duplicated here
- **Full live inventory (curated + related)**: OS-009 Mission Dashboard → Skill Centre portal → SEO/AEO (`portal.html#seo`) — "Skills" = the 7 above (dispatched, in domain law); "Related skills" = all 29 claude-seo plugin skills/extensions auto-discovered from the plugin cache, not yet individually curated. Promote a related skill to curated by adding it to `curated_skills` in `OS-009/app/skill_centres.py`.
- **Most relevant cross-domain global skills**: `meta-find-skills`, `research-notebooklm`, `deep-research`, `research`, `og-deploy`

---

## Notes for the next session

Last action: full skill-registration audit against domain law (§3/§4) — every installed skill now has an explicit dispatch trigger, no orphaned tools. Next action: pilot audit on a real property — needs a fresh session (plugin loads then), Google Cloud API key (PSI, Tier 0) + GSC OAuth (Tier 1). Open question: which property is the pilot (steveapps.co? tartak?).
