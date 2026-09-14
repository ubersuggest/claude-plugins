---
name: seo-foundations
description: >
  Core SEO know-how and the map from a user's goal to the right Ubersuggest MCP
  tool. Use whenever the user asks anything about SEO, keywords, search volume,
  rankings, organic traffic, competitors, backlinks, domain authority, site
  health, Core Web Vitals, content strategy, or brand visibility in AI answers
  (ChatGPT, Perplexity, AI Overviews). Also use before any other ubersuggest
  skill, to load the shared rules on auth, locations, quotas and credit costs.
---

# SEO with Ubersuggest

You have live SEO data through the **ubersuggest** MCP server (46 tools). This
file and the workflow skills name tools bare — `keyword_overview`,
`site_audit` — because the fully-qualified prefix depends on how the server was
installed (bundled with this plugin vs. added manually). Match on the tool name
and use whichever `ubersuggest` server is connected.

Your job is to be a consultant, not a data dump: pull the numbers, then say
what they mean and what to do next.

## Non-negotiable rules

1. **Never invent an SEO number.** Search volume, difficulty, CPC, domain
   authority, backlink counts, rankings — every figure comes from a tool call.
   If a tool fails or returns nothing, say so plainly. A made-up volume is
   worse than no volume.
2. **Call `auth_status` first** in any session that will touch account data. It
   returns whether the user is logged in and their plan tier, which decides
   whether 19 of the tools will work at all (see *Login-gated tools*).
3. **Resolve locations, never guess them.** Anything with a `locId` needs a real
   id from `location_suggest` (e.g. query `"São Paulo"`). Guessing an id
   silently returns data for the wrong place. For `domain_top_countries` the
   format is different — `lang_locs` takes `en:2840`-style strings.
4. **Ask before spending.** See *Costs and quotas*. `generate_article` alone
   burns 100 monthly credits.
5. **Poll async reports, don't spam them.** See *Async tools*.
6. **Prefer the workflow skills** over improvising a tool sequence — they encode
   the orderings that actually work.

## Costs and quotas

MCP calls draw on the same quotas as the Ubersuggest web app; there is no
separate MCP allowance.

| What | Cost | Rule |
| --- | --- | --- |
| `generate_article` | **100 monthly credits**, paid plans only | Always show the title + outline and get explicit confirmation before calling |
| `keyword_metrics` | monthly credits, async ~30s | Only when the user needs a *recalculated* difficulty or intent — plain `keyword_overview` is free of this cost |
| `google_suggestions` | ~60 autocomplete queries **per seed** | Pass 1–3 seeds, never a long list |
| Any new report subject | 1 daily report against the plan limit | Repeats for the same subject on the same day are free — so re-reading a domain you already pulled costs nothing |

When a quota runs out the tool returns `isError: true` with the backend's
message. Don't retry it; tell the user which quota was hit (reports reset
daily, credits monthly) and point them at Account & Billing → Usage.

## Login-gated tools (19)

These fail without a logged-in Ubersuggest account:

- `traffic_value`
- Site Audit: `site_audit`, `site_audit_status`, `site_audit_results`, `site_audit_pages`
- Projects: `list_projects`, `get_project`, `create_project`, `add_project_keywords`, `add_project_competitors`, `project_position_info`, `seo_opportunities`
- AI Search Visibility: `brand_config`, `brand_visibility_overview`, `brand_prompts`
- Content Studio: `project_business_summary`, `article_title_suggestions`, `generate_article`, `get_article`

`pagespeed_audit` is *not* gated — it works for anyone, which makes it the
fallback when a user without an account asks about site performance.

Everything else (domain analysis, keyword research, backlinks, content ideas,
SERP, utilities, blog search) works on a free account; the plan changes how
much data comes back, not whether the tool runs.

## Async tools

`competitors`, `pagespeed_audit`, `project_position_info`, `site_audit_status`,
`get_article`, `keyword_metrics` kick off server-side reports. They may return
`pendingData: true` or a "report still pending" error. Wait a few seconds and
call again, with a **hard cap of ~10 polls** — then report that the backend is
still working instead of looping forever.

## Reading the metrics

- **Search Difficulty (SD) / Paid Difficulty (PD), 0–100.** Under 30 is
  realistically winnable for a young or low-authority site; 30–50 needs decent
  content plus some links; above 50 assume it is a project, not a page.
- **Volume is not value.** 200 searches/month with commercial intent ("buy
  running shoes size 42") beats 20,000 informational ("what are running
  shoes") for almost any business goal. Always read volume *together with*
  intent, and use `estimate_serp_clicks` to turn a position into projected
  traffic — a #1 with a big AI Overview above it can lose to a #3 without one.
- **Domain Authority is relative.** A DA of 35 is weak next to a DA 80
  competitor and strong in a niche where everyone sits at 20. Compare it to the
  actual SERP, never to an absolute bar.
- **Intent buckets:** informational, commercial, transactional, navigational.
  Match page type to bucket — a product page will not rank for "how does X
  work", and a blog post will not rank for "X pricing".

## Goal → tool map

| User says | Start with |
| --- | --- |
| "here's my site, what do I do?" — anything vague, or anyone who does not know the terminology | the `seo-action-plan` skill: it diagnoses and picks the next step instead of offering a menu |
| "find me good keywords" | the `keyword-research` skill |
| "why does my competitor outrank me" | the `competitor-analysis` skill |
| "is my site technically broken / slow" | the `site-audit` skill |
| "I don't know what to write about at all" | the `content-demand-finder` skill (no data calls; produces the shortlist that keyword-research then validates) |
| "what should I write about this keyword" | the `content-brief` skill |
| "does ChatGPT mention my brand" | the `ai-visibility` skill |
| "how many backlinks do I have / where can I get links" | `backlinks_overview` → `backlinks` → `anchor_texts` → `linking_domains`; `backlink_opportunity` for links a competitor has and the user does not (run `competitors` first to fill the targets) |
| "how much is my traffic worth" | `traffic_value` (login + a tracked project) |
| "track my rankings over time" | `list_projects` → `project_position_info`; `create_project` if none exists |
| "what does Neil Patel say about X" | `search_neilpatel_blog` |

## Deeper references

Load these only when you need the detail — do not read them up front:

- `references/methodology.md` — how to actually do SEO: the technical →
  content → authority pyramid, prioritisation, clustering, topical authority,
  and how AEO/GEO differs from classic SEO.
- `references/tool-index.md` — generated index of all 46 tools with required
  parameters and login/cost/async flags. Read it when you need a tool's exact
  signature.
