# SEO Engagement Kickoff Prompt (reusable)

Copy, fill, paste into a Claude Code session opened in `~/OG/dev/OS-017-SEO-Domain/`:

---

/og-project OS-017 — new SEO engagement.

**Property**
- Website URL: <https://…>
- Business model: <e-commerce / services / SaaS / content / local>
- CMS / framework: <Shopify / Next.js / static / WordPress …>

**Market**
- Target audience: <who buys / who reads>
- Geography & languages: <DE / PL / FR / UK / US …>

**Goals**
- Primary goal: <leads / sales / bookings / AI citations>
- Desired outcome in 90 days: <specific, measurable>

**Access**
- Google Search Console: <verified? which account>
- Analytics: <GA4 / Plausible / none>
- Site repo / deploy access: <path or "client-managed">

**Known problems**
- <anything already suspected: traffic drop, migration, thin content, not cited by AI …>

Set up the engagement: create `properties/<domain>/` from `templates/property/`, fill
`context.md` from the above, sync it to the site repo as `.agents/product-marketing.md`,
collect baseline data (GSC export, crawl, AI prompt-set run), then run the diagnostic
audit workflow from `docs/seo-domain-design.md` §Workflow.

---
