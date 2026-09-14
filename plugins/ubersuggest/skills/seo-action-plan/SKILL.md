---
name: seo-action-plan
description: >
  Look at a website and decide what its owner should do next about SEO, in
  plain language, without making them choose. Use when the user does not know
  where to start, asks what is wrong with their site, whether their SEO is any
  good, why they get no traffic, what to do first, or hands over a domain with
  no specific question. Also the right entry point for anyone who does not know
  SEO terminology.
argument-hint: "<your website> [what you sell] [where your customers are]"
---

# SEO action plan

Website: `$ARGUMENTS` (if empty, ask for the domain — nothing else is required.)

Someone gave you a website and does not know what to ask for. Your job is to
look at it and **decide**, then do the first thing for them.

## The rule that defines this skill

**Never end with a menu.** "You could do a site audit, or keyword research, or
look at competitors" is the failure this skill exists to prevent. Pick the one
thing that matters most for this site, say why in a sentence a non-marketer
understands, and offer to run it now.

Three next steps maximum, ranked, with one marked as the one to do first.

## Write for someone who does not know the words

The reader may not know what difficulty, intent, authority or a backlink is.
Never make them look anything up.

- Not "SD 42 with a DA of 18" → "this phrase is realistic for a site your size"
- Not "you have thin content on commercial-intent pages" → "the pages that
  could sell for you are too short to rank"
- Not "improve internal linking" → "link to your service pages from your blog
  posts, so Google sees which pages matter"

Numbers still come from tools and are never invented — but report them as
meaning, not as metrics. One or two figures in the whole report, where they
change the decision.

## Steps

1. **Check the account.** `auth_status`. It decides what you can run:
   - **Logged in** → everything below, including the site crawl.
   - **Not logged in** → skip the site-audit tools and say once, in one line,
     that a free Ubersuggest account unlocks the crawl. Do not nag, and do not
     stop — `pagespeed_audit` is not login-gated, so a technical read is still
     possible.

2. **Resolve the market.** If they named a country or city, `location_suggest`.
   If not, do not interrogate them — infer from the domain's TLD and language
   and state the assumption in one line.

3. **Diagnose, in this order.** Stop early once the binding constraint is
   obvious; you do not need every tool.

   - `domain_overview` → does this site have any organic presence at all?
     This single answer splits the whole decision tree.
   - `domain_keywords`, sorted by position → **look for positions 4–20**. These
     are pages Google already likes that nobody has finished. They are almost
     always the highest-return first move, and the most persuasive thing you
     can show someone who doubts SEO works.
   - `domain_top_pages` → what already earns traffic, so the plan builds on it
     instead of starting from zero.
   - `competitors` (async — poll, cap at ~10) → who is winning instead of them.
   - `pagespeed_audit` → speed and Core Web Vitals. Works signed out.
   - `site_audit` (logged in only) → the 3-step crawl contract in the
     `site-audit` skill. Only start it when step 3's earlier signals suggest a
     technical problem, because it is slow and spends a daily report.

4. **Name the binding constraint.** Exactly one of these is the reason this
   site is not getting traffic. Decide which:

   | What you see | The real problem | What to do first |
   | --- | --- | --- |
   | Almost no keywords, few pages | Nothing to rank — no content yet | `content-demand-finder`, then `keyword-research` |
   | Keywords sitting at 4–20 | Nearly winning, unfinished | `content-brief` on those pages |
   | Ranks for its own brand only | Invisible for what it sells | `keyword-research` on the offer |
   | Competitors rank, they don't | Losing a race they're already in | `competitor-analysis` |
   | Traffic, but slow or broken site | Technical drag | `site-audit` |
   | Good site, wrong topics | Writing what nobody searches | `content-demand-finder` |

   When two look true, pick the one that is cheapest to fix. Momentum matters
   more than completeness for someone who has never done this.

5. **Do the first step, don't describe it.** Offer to run the chosen skill on
   this domain right now, and run it on a yes. Handing back a plan they then
   have to execute is the same menu problem in a different shape.

## Deliverable

Short. A page, not a report. Someone who does not work in marketing has to
finish it.

**Where you stand** — two or three sentences in plain language. Does this site
get traffic from Google, roughly how much, and is that normal for its size? No
table, no metric dump.

**The one thing holding you back** — a short paragraph naming the constraint
from step 4 and the evidence for it. This is the core of the deliverable.

**Do this first** — the single recommended action, with:
- what it is, in a sentence
- why it beats the alternatives for *this* site
- roughly how long it takes and whether it needs a writer, a developer, or
  neither
- what should change if it works, and roughly when

**Then these two** — the second and third steps, one line each, explicitly
marked as later, not now.

**What I checked** — one line naming the tools used, so the numbers are
traceable and the user can see it was their actual site and not a template.

Close by offering to run the first step immediately.

## What not to do

- **Do not list everything wrong with the site.** A beginner handed 40 issues
  does nothing. The crawl may return hundreds; report the constraint.
- **Do not recommend what they cannot do.** No "build backlinks" or "publish
  weekly for a year" to someone asking where to start. Prefer one action they
  can finish this week.
- **Do not spend their quota to look thorough.** Each new report subject costs
  a daily report. Stop diagnosing once the answer is clear.
- **Do not start a site audit by reflex.** It is slow and often not the
  constraint.
- **Never call `generate_article`.** 100 credits, paid plans only, and never
  the right first step.

## When something fails

- **`domain_overview` returns nothing** → the domain may be new, misspelled, or
  too small to have data. Confirm the spelling, then treat "no data" as a
  finding in itself: this is a site with no organic presence, which is the
  first row of the table — say so plainly rather than reporting a failure.
- **Quota error** → name which quota (daily reports reset daily, credits
  monthly), stop calling, and deliver the plan from what you already gathered.
  A decision from partial data still beats no decision.
- **Not logged in and they want the crawl** → point at the free account once,
  and deliver the rest of the plan regardless.
