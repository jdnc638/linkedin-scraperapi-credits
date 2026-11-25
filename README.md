# LinkedIn Scraper Pricing: What 30 Credits per Page Actually Buys, Why Experience and Education Come Back Empty, and Which ScraperAPI Plan Fits Your Volume

ScraperAPI bills a LinkedIn page at **30 credits per request**, so the free plan's 1,000 credits cover roughly **33 profile pages**. It has no LinkedIn-specific parser and no field schema: you send a profile URL through the general-purpose API with `render=true` and get back HTML, markdown or text, then pull the fields out yourself. And since November 13, 2025, the work history and education sections most people want from a LinkedIn scraper are largely missing from public profiles anyway, at roughly a 2% fill rate.

The rest of this page is about the two numbers that decide whether ScraperAPI works for you: how many credits a realistic LinkedIn job burns, and what you can still extract after LinkedIn's field restrictions.

> **Quick verdict:** run 10 to 20 of your own target URLs on the free tier first, because LinkedIn success rates depend on the specific pages you hit. Once that works, size your plan by profile count at 30 credits each, not by marketing copy. Most recruiting or sales lists of a few hundred profiles a month fit the entry paid tiers; anything above roughly 5,000 profiles a month needs the higher concurrency plans.
>
> 👉 [See ScraperAPI's current plan lineup and credit allowances](https://www.scraperapi.com/pricing?fp_ref=coupons)

## ScraperAPI's plans, and what each one changes for LinkedIn work

ScraperAPI sells credits rather than requests, and the tier you buy changes three things: the monthly credit allowance, how many requests can run at once, and what happens when you run out. Prices and allowances move, so the pricing page is the only place to read the number before you buy.

| Plan | Billing options | Concurrency | Price | Get it |
| --- | --- | --- | --- | --- |
| Free | — | 5 connections | $0, includes 1,000 credits | [Start free](https://www.scraperapi.com/?fp_ref=coupons) |
| Hobby | Auto-upgrade | Not published | Listed on the pricing page, monthly or annual | [View Hobby](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | Auto-upgrade | Not published | Listed on the pricing page, monthly or annual | [View Startup](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | Auto-upgrade | Not published | Listed on the pricing page, monthly or annual | [View Business](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | Auto-upgrade, pay-as-you-go | Up to 200 threads | Listed on the pricing page, monthly or annual | [View Scaling](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | Auto-upgrade, pay-as-you-go | Not published | Listed on the pricing page, monthly or annual | [View Professional](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | Pay-as-you-go | Not published | Listed on the pricing page, monthly or annual | [View Advanced](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Pay-as-you-go, custom trial | Customisable to 1,000+ threads | Quoted | [View Enterprise options](https://www.scraperapi.com/pricing?fp_ref=coupons) |

Two billing details matter more than they look. Auto-upgrade moves you to the next tier when credits run out, and it exists on Hobby through Professional. Pay-as-you-go lets you keep scraping past your allowance at a fixed per-credit rate with a monthly cap you set yourself, and it only exists on Scaling, Professional, Advanced and Enterprise. If your LinkedIn volume spikes in bursts, the PAYG tiers are the ones that won't stall mid-project.

Annual plans can also renew early for a fresh batch of credits, which is worth knowing if you're planning a one-off sourcing push rather than a steady pipeline.

## What a LinkedIn scraper on ScraperAPI actually returns

You get the page, not a parsed profile. The API takes `url`, `country_code`, `render`, `output_format` (markdown or text), `premium`, `ultra_premium` and `device_type`. There is no LinkedIn dataset ID, no field list, no built-in CSV of name, title, company and education. For each request you receive the page content, and your script handles extraction and any structuring into JSON.

That's a real difference from purpose-built LinkedIn scrapers, and it decides who should care. If you already have a parser and just need LinkedIn to stop blocking you, ScraperAPI is a clean fit. If you want a JSON array of 40 profile fields without writing extraction code, it isn't that product.

There is one more piece worth knowing: DataPipeline endpoints let you schedule and manage scraping jobs programmatically with webhook delivery, which is how you'd keep a lead database or talent pool synced without a cron job of your own. ScraperAPI quotes 1 to 5 seconds per request on average, with complex pages like job listings or large profiles usually inside 10 seconds.

## The wall you'll hit on experience and education

This part applies to every LinkedIn scraper, not just this one. Since **November 13, 2025**, LinkedIn restricted public access to the **Position**, **Experience** and **Education** fields. Fill rates for those three dropped from 50–64% to roughly **2%**, and they now come back as cached "sticky" data rather than a fresh scrape. Separately, `current_company.industry` has been unsupported since **August 7, 2025**.

Practical consequence: a public profile page no longer reliably renders a full career history, so a scraper that reads the public page can't return one. If a vendor promises complete work history and education, ask two questions. Is the data live or served from cache, and what's the current fill rate on those fields? A vendor that publishes a field status table and flags which columns were backfilled is telling you something useful. One that lists "experience, education" in a feature grid without qualification is probably repeating a claim written before November 2025.

If your project is career-path research or education-to-occupation analysis, this changes the scope of the work. Current title, company, location, follower counts, about text and posts are still there. Multi-year job histories mostly aren't.

## Doing the credit math before you pay

The conversion is simple once you know that LinkedIn sits in ScraperAPI's custom-priced tier at 30 credits per request, against 1 credit for a standard page, 5 for Amazon and 25 for Google or Bing. If a site sits behind Cloudflare, Datadome or PerimeterX and you need the bypass, add 10 credits on top.

| Job size | Credits at 30 per profile | What it means |
| --- | --- | --- |
| 33 profiles | 1,000 | The entire free allowance |
| 500 profiles | 15,000 | A single recruiting sprint |
| 2,000 profiles | 60,000 | A mid-size sales or research list |
| 10,000 profiles | 300,000 | Needs a high-tier plan or PAYG |

Two controls keep this from running away. A `max_cost` parameter caps what any single scrape can spend, and the Domain Cost Estimator in the dashboard shows the real cost for a specific URL before you commit a batch to it. Retries caused by concurrency limits cost nothing extra: exceeding your plan returns a 429 that asks you to slow down, and the request is turned away rather than queued and billed.

👉 [See what 1,000 free credits cover at 30 credits per profile](https://www.scraperapi.com/pricing?fp_ref=coupons)

## Choosing a tier by what you're actually doing

**Testing whether LinkedIn will load at all.** Free plan, 5 concurrent connections, 1,000 credits. That's 33 pages, enough to find out whether your target profiles come back complete or half-empty before you spend anything. Do this first, because field availability varies by profile and by region.

**A one-off list of a few hundred to a couple thousand profiles.** The entry paid tiers carry you through a single sourcing sprint. Turn on auto-upgrade so a bigger-than-expected list doesn't stop at 60% completion, and accept the next tier's price rather than babysitting the account.

**A recurring monthly pipeline.** Scaling gives you up to 200 concurrent threads plus PAYG with a monthly cap. For recruiters pulling fresh candidates weekly or a sales team refreshing account lists, the concurrency is what separates a two-hour job from an overnight one.

**Enterprise-scale or agency work.** Concurrency is customisable past 1,000 threads, and ScraperAPI offers a custom trial with 300+ concurrent threads and up to 50M credits. That's the only path where a Slack channel and premium support are part of the deal.

👉 [Run your first LinkedIn URLs through ScraperAPI's free credits](https://www.scraperapi.com/?fp_ref=coupons)

## Where it breaks, and what to do about it

**Private and restricted profiles.** Nothing on the public web means nothing to scrape. Profiles with strict privacy settings return partial data, and profile URLs must follow the standard `linkedin.com/in/username` pattern or the request is wasted.

**Contact details.** Emails and phone numbers appear only when the profile owner made them public. A scraper can't surface a hidden email, and any tool claiming otherwise is guessing at patterns.

**429 responses.** These mean you're over your plan's concurrency, not over your credits. Reduce parallel requests or move up a tier.

**Parsing, not scraping, is your bottleneck.** Because ScraperAPI hands you page content, budget engineering time for extracting fields and handling layout changes. Markdown output reduces the mess compared with raw HTML but doesn't give you a schema.

**Discovery is a separate problem.** ScraperAPI returns pages you ask for. Building a list of profiles to ask for is a different task, typically done with search engine queries restricted to LinkedIn profile URLs, then validated before you spend 30 credits each on them.

## How the alternatives differ

Bright Data runs the opposite model: structured records, not page content. You send a LinkedIn URL with a dataset ID (separate IDs for profiles, companies, jobs and posts) and get back JSON, NDJSON, CSV or Parquet, with delivery to S3, Snowflake, Azure, GCS or a webhook. Billing is per successful record, one credit per profile, and new accounts get 5,000 free credits monthly without a card. Its API also returns 42 top-level fields on a profile, and publishes a field status table plus a `backfilled_columns` flag showing which values came from cache. That transparency is rare and directly relevant to the experience and education problem above.

LinkdAPI takes a third route: an open-source Python CLI under the MIT licence that wraps its API in a menu-driven interface, aimed at recruiters who don't write code, exporting to CSV or JSON with built-in retry logic for 429s. Its documentation lists experience and education as supported fields, which conflicts with LinkedIn's November 2025 restriction. Treat the field list as written before that change and verify fill rates yourself before relying on it.

ScraperAPI's advantage in that comparison is breadth and price per page across many sites, plus the ability to point one API at LinkedIn, job boards, company sites and Google results without separate contracts. What you give up is the pre-built LinkedIn schema.

## One legal note worth thirty seconds

Public profile data has been treated differently from logged-in data in US litigation, but LinkedIn's terms still prohibit automated access, and GDPR and CCPA apply to personal data you store. Scraping public pages at scale is a business decision with legal exposure attached, not a purely technical one. If you're building a commercial product on the output, get advice rather than relying on a scraper's marketing page.

## FAQ

**Can ScraperAPI scrape LinkedIn?**
Yes, as a general web scraping API pointed at LinkedIn URLs with rendering enabled. It returns page content, so it's a fit if you have your own parser and a poor fit if you want ready-made profile JSON.

**How many credits does one LinkedIn profile cost?**
30 credits per request, plus 10 if bot-protection bypass is needed. A standard page costs 1 credit, so a LinkedIn profile is 30 times the price of a blog post.

**Why can't I get work experience or education?**
LinkedIn restricted public access to Position, Experience and Education on November 13, 2025. Fill rates fell to roughly 2% and the remaining data is served from cache. No scraper reading public pages can restore what LinkedIn stopped rendering.

**Is there a free trial?**
Yes. 1,000 credits with a maximum of 5 concurrent connections, which works out to about 33 LinkedIn pages.

**Can I keep scraping after my credits run out?**
On Scaling, Professional, Advanced and Enterprise, pay-as-you-go continues at a fixed per-credit rate up to a monthly cap you set. On Hobby through Professional, auto-upgrade moves you to the next tier instead.

## What to do next

Match the plan to the shape of your work. Thirty-three pages to test an idea, take the free credits. A few hundred to a couple thousand profiles in one push, an entry paid tier with auto-upgrade on. A weekly or monthly pipeline, Scaling for the 200 threads and the monthly cap. Agency or enterprise volume, ask for the custom trial before committing.

Two things to confirm before you enter card details. First, run 10 to 20 of your real target URLs through the free tier and check how many come back with usable data, since one region's profiles can behave differently from another's. Second, work out your monthly profile count at 30 credits each and compare it with the allowance on the tier you're considering, not the tier above it.

👉 [Compare ScraperAPI's plans and start on the free credits](https://www.scraperapi.com/pricing?fp_ref=coupons)
