# SEO Scout — recurring intelligence sweep (spec)

> Contract for the ongoing "what's hot in SEO/AEO" scout. Runs as a **Hermes cron on the
> Mac Studio** (same pattern as `research-video-inbox`: unattended cycle, dry-run before
> commit). This file is the spec Hermes implements — it syncs via `~/OG/` so the Mac
> Studio session can pick it up directly. Instance of the generic **intelligence loop**
> (`~/OG/ai-os/skill-centres.md` §Intelligence loop) — clone for any centre by swapping
> §Beat and §Assimilation targets.

## Cadence

Weekly (suggest Mon 06:00 CET — digest ready with morning coffee). Monthly deep pass in
week 1 (adds the NotebookLM report, see `notebooklm-standing-prompt.md`).

## The beat (what to watch)

1. Google Search updates + AI Overviews / AI Mode changes (Search Central blog, SERoundtable)
2. AI-crawler behaviour changes (GPTBot/ClaudeBot/PerplexityBot/OAI-SearchBot — new agents, robots semantics, JS execution)
3. GEO/AEO measurement: share-of-answer tooling + methodology (SparkToro, Profound/Peec/Otterly moves)
4. Schema/entity: schema.org changes, rich-result deprecations, knowledge-graph practice
5. claude-seo plugin releases + the skills.sh SEO leaderboard (our engine's upstream)
6. Contrarian signal: what practitioners report NOT working (r/SEO, r/bigseo, HN)

## Execution (Hermes side)

- Runner: Hermes scout research agent (MiniMax-backed scout if configured on the Studio —
  verify agent name at install; fall back to a plain web-research agent with
  `last30days`-style sweeps). One run = one sweep over §Beat with per-item source URLs.
- **Verification rule**: every claim carries a source link + date; anything unverifiable
  is marked speculation. No stat enters a digest unsourced (the Neil Patel lesson —
  `../playbooks/aeo-neil-patel-playbook.md`).

## Output contract (per run)

1. **Digest file** → `~/OG/dev/OS-000-SEO/docs/intelligence/digests/YYYY-MM-DD-seo-scout.md`
   — max 1 page: 3-7 findings, each = claim · source+date · "so what for OS-000-SEO" ·
   proposed action (`none | playbook edit | domain-law change | tool change`).
2. **Google Doc** → OS-000-SEO Drive store `research/` folder (id in project CLAUDE.md) via
   `gws docs`, same content — Phil's readable/commentable copy.
3. **Broadcast candidates** → the digest ends with **1-2 "noise" items**: findings
   interesting enough for a social post, each as a 2-3 sentence draft hook (plain voice,
   no hype — run through `meta-humanizer` before any actual posting). These feed the
   brand floor's posting queue. We need to be seen making noise; the scout supplies the
   raw material every week.

## Assimilation (human-gated, in a Claude Code session)

Weekly, when reviewing the digest: proposed `playbook edit` → apply to
`docs/playbooks/*` and commit; `domain-law change` → edit `seo-domain-design.md` with
the evidence cited; cross-centre lesson → `/capture` to the vault. **The scout proposes;
the session (with Phil) disposes.** Digests are append-only history; the playbooks are
the living state.

## Install (Hermes, one-time — pending)

On the Mac Studio Hermes session: register the weekly cron per the research-video-inbox
pattern, pointing at this spec. Until installed, the sweep can be run manually from any
session ("run the SEO scout sweep per docs/intelligence/seo-scout-spec.md").
