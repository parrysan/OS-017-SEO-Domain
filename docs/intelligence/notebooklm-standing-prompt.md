# NotebookLM standing prompt — "State of SEO/AEO"

> The carefully-written, versioned prompt run against the OS-017 NotebookLM notebook to
> generate recurring field reports. NotebookLM's strength: it reasons over the **curated
> source pile** (everything the scout + Phil feed it), so reports compound as sources
> accumulate. Managed via the `research-notebooklm` skill (provision an `OS-017-SEO-Domain`
> notebook on first use; scout digests, key articles, and video transcripts get pushed as
> sources continuously).

## Cadence

Monthly (week 1), after the scout's deep pass — the report reads over everything
ingested since the last run. Output lands in `docs/intelligence/digests/` as
`YYYY-MM-notebooklm-state-of-seo.md` + a Google Doc in the Drive store.

## The prompt (v1 — 2026-07-04; version this file on every change)

```
You are the research analyst for a solo digital studio's SEO/AEO practice serving
small-business clients in Europe (PL/DE/FR/UK) and e-commerce brands. Using ONLY the
sources in this notebook, produce a "State of SEO/AEO" report with these sections:

1. WHAT CHANGED — the 5 most consequential developments since the previous report
   (search engines, AI answer engines, crawlers, measurement tools). For each: what
   happened, source, and the direct implication for a small-agency practice.
2. WHAT'S OVERHYPED — 3 currently-loud tactics the sources suggest are weak, unproven,
   or already deprecated. Be specific about the evidence.
3. WHAT'S UNDERPRICED — 3 tactics with strong evidence but little attention, viable for
   a one-person operation.
4. LAW CHECK — evaluate these standing operating assumptions against the sources and
   flag any that now look wrong or outdated: (a) AI crawlers do not execute JavaScript;
   (b) llms.txt is ignored by Google and matters only for docs/dev-tool sites;
   (c) "AI rank position" is statistically meaningless — track share-of-answer against
   a fixed prompt set instead; (d) optimal AI-citation passage length is a
   self-contained 134-167 words; (e) for AI Overviews, classic top-10 Google ranking
   remains the entry ticket; (f) Organization+sameAs entity coherence is the highest-
   leverage schema work.
5. CLIENT TALKING POINT — one finding, explained in two plain-language sentences a
   non-technical business owner would find genuinely interesting.
6. NOISE CANDIDATES — 2 findings worth a social post, each as a 2-3 sentence draft
   in a factual, no-hype voice.

Rules: every claim cites a notebook source. Distinguish measured findings from vendor
claims. If sources conflict, say so and weigh them. Maximum 2 pages.
```

## Section 4 is the engine

The LAW CHECK list must mirror the current assumptions in `seo-domain-design.md`. When
the domain law changes, update the list here in the same commit — that's what makes the
notebook actively police our own doctrine instead of just summarizing news. **Reuse note
for other centres**: this LAW CHECK pattern (enumerate your standing assumptions, make
the report attack them monthly) is the most portable piece — every skill centre's
notebook prompt should have one.
