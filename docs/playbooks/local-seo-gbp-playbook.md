# Local SEO / GBP Playbook

> Distilled 2026-07-04 from "AIOS SEO Strategies" (Alventra Marketing's 20-prompt local-SEO
> stack; source archived in OG-Research/OS-017/research/). Adapted to this domain's
> architecture — their browser-scraping execution model is replaced by our API/agent stack.
> Applies to any property where `context.md` says **Local SEO relevant: yes**.

## Why this matters for OGANIKO Digital

Lane 1 clients are local SMBs (garden centre, sawmill, trades). For them the **map pack,
not the organic SERP, is where revenue lives** — and GBP work is faster to show results
than site work (category fixes can move rankings within days).

## Core lessons adopted

1. **Context-first is everything.** Their "load business context once, reference forever"
   = our `context.md` contract, extended with a Local SEO block (GBP URL, NAP, service
   areas, competitor GBP URLs, average job value, review baseline). Generic output is a
   missing-context bug, not a model bug.
2. **Categories before everything.** Wrong GBP categories = invisible for high-intent
   searches. Always the first local audit step.
3. **Table stakes vs differentiator.** For categories, attributes, services: what ALL top
   competitors have is non-negotiable; what one has is a differentiation opportunity.
   This classification pattern applies to every comparative audit.
4. **Review velocity > review count.** 90 reviews at 15/month beats 200 stale ones.
   Deliverable per client: reviews-per-month target + keyword-rich response templates
   (responses are owner-controlled GBP content — ~120 keyword placements/year at 10
   reviews/month).
5. **Owner-controlled text fields are prime real estate**: services descriptions,
   750-char business description (write 3 versions, test in 30-day windows), posts.
   Cross-reference services section against the website — drift here is common and costly.
6. **Neighborhood relevance compounds**: posts/photos naming specific areas build
   location association that is hard to replicate. Photo *velocity* beats photo volume.
7. **Page-2 goldmine**: GSC keywords at position 11–20 with ≥100 impressions/month are
   the highest-ROI optimisation targets on the website side.
8. **Stage-4 first**: map keywords to buyer journey (problem-unaware → ready-to-hire);
   ready-to-hire terms convert 5–10x — they go on service pages + GBP before anything else.
9. **Review sentiment mining**: competitors' reviews contain the emotional language and
   money phrases customers actually use — feed into site copy, GBP description, and
   review-request scripts (pairs with `meta-humanizer`).
10. **Report calls, not vanity**: monthly report = GBP calls + direction requests +
    organic conversions, 3 wins / 3 problems / 1 next action, readable in 5 minutes.
    (Matches our W4 KPI stack; adds the GBP insights block for local clients.)

## Their 20 prompts → our execution

| Their prompts | Our executor | Notes |
|---|---|---|
| 1–2 GBP categories + attributes | `claude-seo:seo-local` + `seo-maps` | table-stakes classification in output |
| 3–4 reviews teardown + response system | `seo-local` (review intelligence) + templates via `meta-humanizer` | velocity target is the deliverable |
| 5, 19 posts strategy + pattern analysis | `seo-local` + content calendar in plan | 2–3 posts/wk, neighborhood mix |
| 6–8 services / description / photos | `seo-local` + `seo-visual` | description: 3 test versions |
| 9, 16, 17 keyword gap / intent map / content gap | `seo-cluster`, `seo-dataforseo` (when funded), `content-gap-agent` | stage-4 first |
| 10, 12 money pages + GSC page-2 | `seo-google` (GSC API) | pos 11–20 × ≥100 impressions filter |
| 11 service+city pages | `seo-programmatic` / `programmatic-seo` | thin-content safeguards apply |
| 13 review sentiment | `seo-content` + copy work | customer-language rewrite |
| 14 backlink gap | `seo-backlinks` | domains linking to all competitors first |
| 15 citations / NAP | `seo-maps` (cross-platform NAP verification) | red-flag inconsistencies; 30-day visible wins |
| 18 entity optimisation | `seo-schema` + `ai-seo` | already domain law (Organization + sameAs) |
| 20 monthly report | W4 cycle + report-builder | add GBP insights block for local clients |

## Local engagement sequence (their 12-week order, kept — it's sound)

Wk 1: context + categories/attributes → Wk 2: reviews + posts → Wk 3: services/description/photos
→ Wk 4: keyword gap + GSC page-2 → Wk 5–6: money pages, city pages, sentiment copy
→ Wk 7–8: backlinks, citations, intent map → Wk 9–10: content gaps, entity, post patterns
→ Wk 11–12: first monthly report, double down.

## What we deliberately do differently

- **APIs over logged-in-tab scraping** (their Chrome/Cowork model): GSC via OAuth,
  CrUX/PSI via API, maps data via `seo-maps` tiers. Browser automation only where no API
  exists (GBP competitor surface), and flagged as fragile.
- **Evidence + falsifiability** on every recommendation (domain law) — their prompts
  assert impact levels; we require the "how would we know this failed?" line.
- **Privacy**: client GBP/competitor data lands in `properties/<domain>/data/`, never
  in the public repo.
- Their unverified marketing stats (42% directions, etc.) are treated as directional
  heuristics, not client-facing claims.
