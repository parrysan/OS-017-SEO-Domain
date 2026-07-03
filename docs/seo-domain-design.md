# SEO Domain — Design (OS-017)

> Founding design for the SEO operating environment inside the AIOS. Status: v1, 2026-07-03.
> Research basis: GEO/AEO state-of-the-art briefing (2026), skills.sh registry survey,
> installed-skill contract analysis. Inspired by the "toolkit → identity → audit → report →
> implement" workflow (YouTube: *I Used Claude to Optimise My Site for AI Search & SEO!*),
> hardened into a durable AIOS domain.

---

## 1. SEO domain definition

**The SEO domain owns organic findability** — of any OG/client property — **across both
classic search and AI answer engines** (Google/Bing organic, AI Overviews, ChatGPT,
Perplexity, Claude). It is an operating environment, not a skill: per-property state,
a toolkit of skills/agents, defined workflows, and durable memory.

One system, not two: a 2026 audit is the classic technical audit **plus an AI-access
layer** (crawler/CDN access, raw-HTML visibility, entity/schema coherence, prompt-set
baseline). Google's own line — "GEO is still SEO" — holds for Google surfaces; ChatGPT
and Perplexity add genuinely distinct levers (Bing rankings, Reddit/Wikipedia presence,
no-JS rendering).

### Boundaries

| Domain | It owns | SEO domain's relationship |
|---|---|---|
| **Research** | Market/competitor/query intelligence, deep-dives | SEO *consumes* research (SERP landscape, competitor teardown via `deep-research`, `research`) and *commissions* it with specific questions. SEO owns only search-specific data (GSC, crawls, prompt-set runs). |
| **Design** | IA, page clarity, conversion UX, visual system (ODS) | SEO *diagnoses* (weak IA, unclear entity, poor extractability) and hands design a brief; design decides *how* it looks. SEO never restyles pages. |
| **Development** | Code, templates, schema implementation, deploys | SEO writes **tickets** (finding → fix → acceptance test); dev implements per branch-per-task convention in the site's own repo. SEO validates after deploy. |
| **Documentation / reporting** | Vault, client comms conventions | SEO produces its own reports (audit, monthly) from templates; durable decisions go to the vault via `/capture`, per-property memory stays in `properties/<domain>/decisions.md`. |

The test for "is this SEO-domain work?": *does it change what search/answer engines
find, understand, or cite?* If it changes what humans feel — design. If it changes how
code works — dev. If it answers a market question — research.

## 2. Environment architecture

```
OS-017-SEO-Domain/
├── CLAUDE.md                    # bootstrap manifest (core environment definition)
├── docs/
│   ├── seo-domain-design.md     # this file — domain law
│   └── playbooks/               # per-workflow runbooks as they harden
├── templates/
│   ├── kickoff-prompt.md        # reusable engagement kickoff (see §6)
│   └── property/                # copied per engagement
│       ├── context.md           # identity & positioning contract
│       └── README.md            # folder contract
├── properties/                  # PRIVATE (gitignored) — one folder per engagement
│   └── <domain>/
│       ├── context.md           # → synced to site repo as .agents/product-marketing.md
│       ├── data/
│       │   ├── prompts.txt      # fixed AI prompt set (share-of-answer)
│       │   ├── gsc/             # dated Search Console exports
│       │   ├── crawls/          # dated crawl outputs (squirrel)
│       │   └── analytics/       # GA4/Plausible exports
│       ├── audits/              # dated findings (evidence + ICE scores)
│       ├── plans/               # dated implementation plans (tickets by owner domain)
│       ├── reports/             # client-facing deliverables
│       └── decisions.md         # append-only property memory
├── src/                         # python3-stdlib helpers (prompt-set runner, GSC pull) as needed
└── tests/
```

**Knowledge placement** (AIOS layering): reusable skills → global library
(`~/.agents/skills/`, `~/.claude/skills/`); per-property state → `properties/` (private);
cross-client lessons and pattern decisions → vault via `/capture`; the environment
definition → this repo (public).

**The context contract.** `properties/<domain>/context.md` is copied into the site's own
repo as `.agents/product-marketing.md`. The installed ecosystem skills (`seo-audit`,
`ai-seo`, `programmatic-seo`) read that file automatically before asking questions — the
video's "identity & positioning" phase, made durable and machine-read.

## 3. Specialist agent model

Roles are **dispatch profiles** — a subagent prompt + the skill(s) it runs + declared
inputs/outputs — not separately-installed code. The orchestrator is the Claude session
in this repo; specialists run via the Agent tool (parallel where independent).

**Execution engine:** most technical roles are *executed by* the **claude-seo plugin**
(AgriciDaniel/claude-seo, 10.4K★ — 25 skills + 18 specialist agents, `/seo audit|page|
schema|geo|content|local|backlinks|drift`, parallel sub-agent dispatch, PDF reports).
The table below is the AIOS-side contract: what we dispatch, with what inputs, into
which files — regardless of whether the muscle is claude-seo, an ecosystem skill, or a
plain subagent. Two claude-seo patterns are adopted domain-wide: every recommendation
carries a **falsifiability check** ("how would we know this failed?") + a leading
indicator, and **drift monitoring** (dated snapshots diffed each cycle).

| Agent | Does | Inputs | Outputs | Dispatch when |
|---|---|---|---|---|
| **seo-orchestrator** | The session itself: runs workflows (§4), dispatches specialists, merges findings, applies ICE, owns the plan | `context.md`, prior `decisions.md` | Audit doc, plan, report | Always — it *is* the engagement session |
| **technical-seo-audit** | Crawl + technical sweep: crawlability, rendering (JS vs raw HTML), CWV, canonicals, redirects, sitemap, robots + **AI-crawler/CDN access check** | URL, crawl output (`squirrel`), robots.txt/CDN config | `audits/…-technical.md` findings w/ evidence | Diagnostic audit; quarterly re-crawl |
| **onpage-optimizer** | Titles, metas, headings, content structure, extractability (definition-first, self-contained passages, Q&A blocks) | Crawl pages, `context.md`, target queries | Per-page fix list w/ rewritten elements | After audit; content refresh cycles |
| **schema-agent** | Entity plumbing: Organization + sameAs, FAQPage, Product/Article/Person JSON-LD; NAP/entity coherence across pages | Site pages, business facts from `context.md` | Ready-to-paste JSON-LD + placement tickets | Audit flags weak entity; new site launch |
| **ai-search-agent** | GEO/AEO layer: runs `ai-seo` skill; AI-crawler access, raw-HTML visibility, citation-worthiness, prompt-set baseline | `context.md`, `prompts.txt`, crawl | AI-readiness findings + share-of-answer baseline | Every diagnostic audit; monthly prompt-set run |
| **gsc-analyst** | Pulls & reads Search Console via `gws`: striking-distance queries (pos 4–15 × impressions), decay, coverage errors | GSC property access | `data/gsc/` exports + opportunity table | Baseline; monthly cycle |
| **content-gap-agent** | Query/competitor gap: what target audience asks that the site doesn't answer; commissions `deep-research` for SERP/competitor teardowns | `context.md`, GSC queries, competitor list | Prioritised content brief list | Strategy phase; quarterly |
| **internal-linking-agent** | Orphan pages, link equity to money pages, anchor quality | Crawl graph | Linking fix list (from → to → anchor) | After technical audit; after new content ships |
| **implementation-planner** | Converts confirmed findings into tickets: fix, owner domain (content/design/dev), acceptance test, ICE score, sequenced 60/40 quick-wins/strategic | All audit findings + Phil's priorities | `plans/…-implementation-plan.md` | After every audit review checkpoint |
| **report-builder** | Client-facing narrative: what shipped, KPI trend (conversions, clicks, impressions, share-of-answer), next cycle | Plan, GSC/analytics data, prompt-set results | `reports/…` (md → pdf/doc via existing doc skills) | Audit delivery; monthly |

**Verification pattern:** for audit findings, dispatch finders in parallel, then have the
orchestrator adversarially verify high-impact claims (does the canonical error actually
reproduce? is the page really blocked?) before they reach the plan. No finding enters a
plan without evidence (URL + observed value).

## 4. Workflow design

### W1 — Engagement kickoff (once per property)
1. **Intake** — paste `templates/kickoff-prompt.md` filled in.
2. **Scaffold** — create `properties/<domain>/` from template; fill `context.md`; sync to site repo as `.agents/product-marketing.md`.
3. **Access** — verify GSC via `gws`; note analytics + deploy path; write `prompts.txt` (25–100 fixed prompts from the search-intent map).
4. **Baseline** — parallel: GSC export (gsc-analyst) + crawl (`squirrel`) + prompt-set run (ai-search-agent). Dated files into `data/`.

### W2 — Diagnostic audit
1. Dispatch in parallel: technical-seo-audit, ai-search-agent, onpage-optimizer, schema-agent, internal-linking-agent (each reads `context.md` + baseline data).
2. Orchestrator merges, dedupes, **verifies** high-impact findings, scores ICE — *weighted by revenue proximity, not tool severity*.
3. **Checkpoint: Phil reviews** the audit doc (`audits/`).
4. report-builder produces the client-facing audit report.

### W3 — Implementation
1. implementation-planner writes the plan: tickets by owner domain, acceptance tests, 60/40 quick-wins/strategic for the first 90 days.
2. Dev tickets execute in the **site's repo** (branch-per-task, Codex delegation allowed, og-deploy to ship). Design briefs go to the design domain (ODS). Content briefs to content work.
3. **Validate** — re-crawl changed pages, confirm each acceptance test, log results to `decisions.md`.

### W4 — Recurring optimisation cycle (monthly)
1. Pull fresh GSC + analytics; run the fixed prompt set; CWV + coverage check.
2. Re-score the backlog (striking-distance movement, decay).
3. Ship 2–4 prioritised items (mix: technical fix, content update, entity/schema work).
4. Report within 5 business days of month-end: conversions/AI-referrals → clicks/impressions → **share-of-answer trend** → shipped-work log. Quarterly: full re-crawl + strategy reset.

## 5. Cross-domain integration

- **Research →** SEO commissions `deep-research`/`research` with specific questions
  (SERP landscape for money queries, competitor content teardown, "where does the
  audience actually ask" — Reddit/forums matter: Perplexity over-indexes Reddit ~47%).
  Research outputs land in `properties/<domain>/data/` and feed content-gap-agent.
- **Design →** SEO hands ODS a *problem brief*, never a layout: "money page answers the
  query below the fold", "entity unclear above the fold", "FAQ content exists but isn't
  scannable". Design work runs through `ods` / `design-impeccable` with the brief attached.
- **Development →** every dev-owned ticket carries file-level specificity where possible
  (template, schema block, redirect map) + an acceptance test the SEO domain re-checks
  post-deploy. Shopify properties route through the shopify-plugin skills; static/Next
  through the site repo + `og-deploy`. Hard 2026 rule surfaced to dev early: **AI crawlers
  don't execute JS** — critical content must be in server-rendered HTML.
- **Reporting/memory →** client reports from report-builder; cross-client lessons
  promoted to the vault via `/capture` (never silently); per-property memory appends to
  `decisions.md`.

## 6. Reusable kickoff prompt

Canonical copy: [`templates/kickoff-prompt.md`](../templates/kickoff-prompt.md). Asks for:
URL, business model, target audience, geography/languages, goals + 90-day outcome,
CMS/framework, GSC/analytics access, known problems.

## 7. Definition of done

**Diagnostic audit is done when:**
- Baseline data exists and is dated (GSC export, full crawl, prompt-set run).
- Every finding has: evidence (URL + observed value), impact/effort (ICE) score weighted
  by revenue proximity, and an owner domain.
- The AI-access layer was explicitly checked: robots/CDN bot rules, raw-HTML content
  visibility, Organization+sameAs coherence, share-of-answer baseline recorded.
- High-impact findings were adversarially verified (reproduced, not just tool-flagged).
- Phil reviewed the audit doc; client report delivered from it.

**Implementation plan is done when:**
- Every accepted finding became a ticket with: concrete fix, owner domain, acceptance
  test, **falsifiability check + leading indicator**, sequence position (quick-win vs
  strategic, ~60/40 first 90 days).
- Dev tickets are executable in the site repo without re-reading the audit.
- Nothing generic survived — a ticket that could apply to any website is deleted or made specific.

**An optimisation cycle is done when:**
- Fresh data pulled (GSC, analytics, prompt set) and backlog re-scored.
- 2–4 items shipped and validated (acceptance tests re-checked post-deploy).
- Report delivered within 5 business days of month-end with the KPI stack
  (conversions incl. AI referrals → clicks/impressions → share-of-answer → shipped log).
- `decisions.md` appended; anything reusable across clients drafted for `/capture`.

---

## Toolkit (installed & wiring)

| Layer | Tool | Status |
|---|---|---|
| **Audit engine** | **claude-seo plugin** (AgriciDaniel, 10.4K★) — `/seo` orchestrator, 25 skills, 18 agents, drift monitoring (SQLite), PDF reports | ✅ installed (`claude-seo@agricidaniel-claude-seo`, user scope) |
| Audit reasoning | `seo-audit` (coreyhaines31, 151K installs) | ✅ installed globally (`~/.agents/skills/`) |
| GEO/AEO | `ai-seo` (coreyhaines31, 84K) | ✅ installed |
| Scale pages | `programmatic-seo` (coreyhaines31, 96K) | ✅ installed |
| Lighthouse-grade technical | `seo` (addyosmani/web-quality-skills, 30K) | ✅ installed |
| CWV / performance | **PageSpeed Insights API** (free, 25K queries/day) — claude-seo Tier 0, just a Google Cloud API key | ⏳ create API key at first pilot |
| GSC | claude-seo **Tier 1 OAuth** (GSC + Indexing API); alternative: AminForou/mcp-gsc (1.1K★) | ⏳ run OAuth setup at first pilot; creds land in `~/.config/claude-seo/` |
| Skill discovery | `meta-find-skills` (npx skills / skills.sh) | ✅ installed |
| Research | `deep-research`, `research`, `last30days` | ✅ existing AIOS domain |
| Reporting | claude-seo PDF reports; md → docx/pdf via `anthropic-skills:docx`/`pdf`; slides via `og-design-slides` | ✅ existing |
| AI visibility measurement | scripted prompt-set runner (src/, python3 stdlib) — Otterly ($29/mo) as paid upgrade if a client retainer justifies it | ⏳ build at first pilot |

**Deferred until a client engagement pays for it** (all pre-wired as claude-seo extensions):
DataForSEO ($50 min deposit — cheapest SERP/volume data when needed), Firecrawl (500 free
credits — only for JS-heavy sites), Screaming Frog CLI (£199/yr — only for multi-thousand-page
audits), SE Ranking / Profound extensions. `audit-website` + squirrel CLI stays optional as a
second-opinion crawler (binary not installed).

Not chosen (and why): Profound/Peec-class tools — enterprise pricing, wrong tier for SMB
retainers; "AI rank" trackers — rank order in AI answers is statistically random (SparkToro
2026); track **share of answer** instead. llms.txt — Google formally ignores it; ship only
for dev-tool/docs properties, never sell it as SEO work.

---

## Appendix — the video workflow, mapped

The source video (*Systems Made Better*, 2026-06-20) is a live demo of the claude-seo
plugin. Its five phases map onto this domain as:

| Video phase | This domain |
|---|---|
| 1. Toolkit setup (plugin + GSC OAuth) | Installed once, globally (this doc §Toolkit) — never repeated per client |
| 2. Identity & positioning (brand brief md) | `properties/<domain>/context.md` → synced as `.agents/product-marketing.md`; voice guide via `meta-humanizer` for client-facing prose |
| 3. Run the audit (`/seo audit` + brief) | W2 diagnostic audit — claude-seo does the sweep, AIOS adds verification, ICE-by-revenue scoring, and the AI-access layer checks |
| 4. Report (score + Critical/High-impact plan) | `audits/` + report-builder output in `reports/` |
| 5. Implementation (Claude edits + deploy) | W3 — tickets by owner domain in the *site's* repo, branch-per-task, og-deploy; validation re-crawl closes the loop |

Improvements over the video: durable per-property memory (`decisions.md`), private data
separation, cross-domain handoffs (design/dev/research), recurring W4 cycle with
share-of-answer measurement, and skipping its llms.txt step for non-docs properties.
