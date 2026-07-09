# AEO Playbook — Neil Patel Material, Evaluated

> Distilled 2026-07-04. Neil Patel/NP Digital publishes the most widely-read AEO content
> on the web; evaluated for adoption into the `ai-search-agent` role (see
> `docs/seo-domain-design.md` §3). Verdict: reuse the tactical patterns, skip the stats,
> supplement the technical gaps with domain law already established elsewhere in OS-000-SEO.

## Adoption verdict

**Reuse:**
- Question-header + immediate-answer content pattern (H2/H3 phrased as a question,
  answer in the next 2-4 sentences, directly below) — matches our citability guidance
  in `seo-domain-design.md` (definition-first sentences, self-contained passages).
- FAQ schema discipline — but see the citation-length gap below.
- **Monthly manual-prompt audit habit**: query ChatGPT/Perplexity directly to find your
  own content gaps, before assuming what to write. Cheap, no tooling required.
- Ubersuggest AI Search Visibility (Brand Visibility %, Industry Rank, per-prompt
  visibility) as a low-cost tracking option if already in that ecosystem — not superior
  to Profound/Peec, but viable at zero incremental spend.

**Skip:**
- His stat-drops (60% zero-click searches, "six factors" ChatGPT study, 27% AI-over-search
  adoption) — none carry a traceable source in his own published material. Do not repeat
  these to clients as sourced fact; re-derive from primary studies if needed.
- His self-comparison of AI-visibility tools (predictably favors his own Ubersuggest) —
  read as marketing, not an independent evaluation.
- Treating GBP/NAP hygiene as "AEO" — that's local SEO repackaged under a new label,
  already covered properly in `local-seo-gbp-playbook.md`.

**Gap his material leaves — already covered by OS-000-SEO domain law, not by him:**
- No stance on llms.txt (neither advocates nor debunks it) — our domain law: ship only for
  dev-tool/docs properties, Google formally ignores it.
- No discussion of JS-rendering / AI-crawler access — our domain law: AI crawlers don't
  execute JS, SSR is a hard requirement, checked in every technical audit.
- No entity/knowledge-graph schema depth (no `sameAs`→Wikidata, no `speakable`) — our
  domain law: Organization + sameAs is the highest-leverage entity signal.

**Net assessment**: competent generalist marketing content, useful as an on-ramp and for
the two tactical habits above, but it doesn't compete at the technical depth this domain
already operates at. Don't cite him as a primary source in client deliverables — the
patterns are worth using, the byline isn't worth borrowing.

## The one number worth tracking from his material

**Citation-length gap**, confirmed independently on the oganiko.com pilot audit: his
"answer in 2-4 sentences" guidance under-shoots the empirically optimal **134-167 word**
self-contained passage length (Princeton GEO paper, already in `seo-domain-design.md`).
oganiko.com's own FAQ answers are 15-45 words — extractable but thin, exactly the failure
mode his shorter guidance would produce. Use 134-167 words as the target, not his 2-4
sentences.
