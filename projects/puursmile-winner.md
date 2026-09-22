# PuurSmile — A/B Test Winner Promotion

Embedded Shopify app that promotes the winning variant of a product-page A/B test
onto the live product, with a preview, a backup and a one-click rollback.

## What it does

The CRO team ran A/B tests between two versions of the same product page. When one
won, someone had to copy the content across by hand — title, description, SEO,
collections, variant prices — and a developer had to be involved every time.

This turns that into a three-step flow: pick the winner and the control, review a
field-by-field diff of exactly what will change, confirm. Every promotion writes a
backup first, so any change can be reverted from the History page.

## My role

Sole developer: the app, the Shopify integration, the diff engine, the backup and
restore, the deployment, and the user guide the team works from.

## Stack

Remix · TypeScript · React · Shopify Admin GraphQL API · Polaris · App Bridge ·
Docker · Railway

## Engineering highlights

**Nothing is written before it is shown.** The diff is computed field by field —
including collection membership and per-variant pricing — and the operator has to
type a confirmation before anything touches the live product.

**Backup before every write, restore in one click.** Backups are stored on a
persistent volume and the History page replays them.

**A guard against the expensive mistake.** A protected template can be configured
as off-limits, so the one page nobody wants overwritten cannot be overwritten.

**The awkward details handled, not hidden.** Only manually curated collections can
be synced through the API, so automated ones are skipped and flagged in the diff
instead of failing silently. Promotion matches variants by position across two
different products; restore matches them by ID on the same one — two different
rules, for two different jobs.

## Source code

Private — internal client tooling. Happy to walk through it in a call.
