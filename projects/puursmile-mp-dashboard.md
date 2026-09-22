# PuurSmile — Media Performance Dashboard

Executive analytics dashboard for a Shopify Plus oral-care brand: one place where
marketing spend, revenue, subscriptions and creative performance finally agree.

## What it does

The team was rebuilding a weekly reporting deck by hand, on top of a 19-tab
spreadsheet that had started returning `#REF!`. This replaced both.

Every night it pulls data from twelve sources — Shopify, Meta Ads, Google Ads,
Hyros, Recharge, Amazon, PostHog, Google Sheets and others — recalculates the
numbers the team actually makes decisions on (MER, ROAS, CAC, net profit,
subscription retention), and shows underneath every figure where it came from
and how fresh it is.

## My role

Sole developer: architecture, data model, every integration, the nightly
pipeline, the frontend, the test suite and the deployment.

## Stack

Next.js 15 (App Router) · TypeScript · React · PostgreSQL + Prisma · Tailwind ·
Recharts · Auth.js · Vitest + Playwright · Railway

## Engineering highlights

**Data provenance enforced by the build.** Every block on screen declares which
database columns it derives from, and a test fails the build if a declared column
doesn't exist or isn't written by any job. The lineage can't quietly drift away
from the code.

**A nightly sentinel against silent drift.** The pipeline compares itself against
the managers' own spreadsheet every night, and separates a broken data feed from
a formula that has diverged — two problems that look identical on a dashboard and
need opposite fixes.

**Fault isolation across fourteen scheduled jobs.** A single failing ad account
used to stall the entire ingestion. Writes are now scoped per account and per day,
with retries and backoff, so one bad integration degrades instead of stopping
everything.

**Cross-domain attribution** from pre-lander through to Shopify checkout, built to
coexist with third-party A/B testing rather than fight it.

**Deep Shopify integration:** Admin GraphQL and ShopifyQL, HMAC-verified webhooks,
Liquid snippets and a Web Pixel deployed into the live theme.

## Scale

41 database models · 35 dashboard pages · 14 scheduled jobs · 500+ tests ·
396 commits over four months

## Source code

Private — client work. Happy to walk through the architecture and the trade-offs
in a call.

---

**Nazario De Letteriis** — Lead Full-Stack Developer
[LinkedIn](https://www.linkedin.com/in/nazariodeletteriis) · [letrionlabs.it](https://letrionlabs.it)
