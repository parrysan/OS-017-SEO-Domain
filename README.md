# OS-017-SEO-Domain

> A reusable SEO operating environment inside the AIOS — deep audits, AI-search/GEO/AEO readiness, implementation planning, and reporting, dispatchable per website/property for Oganiko's clients.

## Where to start

- **For working on this project**: read `CLAUDE.md` in this folder. It is the bootstrap manifest — it tells any LLM (or human) which files to read and in what order.
- **For project status, decisions, and history**: see the vault project page at `Open-Memory-Vault/projects/OS-017-SEO-Domain/README.md`.

## Quick facts

- **Project code**: OS-017-SEO-Domain
- **Created**: 2026-07-03
- **GitHub**: https://github.com/parrysan/OS-017-SEO-Domain

## Structure

```
.
├── CLAUDE.md      # bootstrap manifest — read this first
├── README.md      # this file
├── docs/          # domain design, architecture
├── templates/     # property kickoff templates (context, audit, plan, report)
├── properties/    # per-client engagements (gitignored — private)
├── src/           # crawl/parse scripts (python3 stdlib)
└── tests/         # tests
```

All durable knowledge — decisions, research, status narrative — lives in the vault project page, **not** in `docs/`. The code repo holds the environment: skills, templates, scripts, and design docs.
