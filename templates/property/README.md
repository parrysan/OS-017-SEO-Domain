# Property folder contract

One engagement = one folder: `properties/<domain>/`, copied from this template.

```
properties/<domain>/
├── context.md          # identity & positioning — synced to site repo as .agents/product-marketing.md
├── data/
│   ├── prompts.txt     # fixed AI prompt set (share-of-answer measurement)
│   ├── gsc/            # Search Console exports (queries, pages, coverage) — dated files
│   ├── crawls/         # squirrel / crawl outputs — dated files
│   └── analytics/      # GA4/Plausible exports
├── audits/             # YYYY-MM-DD-<scope>.md — findings with evidence + ICE scores
├── plans/              # YYYY-MM-DD-implementation-plan.md — tickets by owner domain
├── reports/            # client-facing reports (monthly / audit report)
└── decisions.md        # append-only log: what was decided, why, result
```

Rules:
- Everything here is **private** (gitignored). Client data never reaches the public repo.
- All data files are **dated**, never overwritten — trend analysis needs history.
- `decisions.md` is append-only; it is the property's memory across cycles.
