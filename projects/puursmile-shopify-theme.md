# PuurSmile — Shopify Theme Engineering

Liquid work on a live, high-traffic DTC store: a dental membership programme that
had to behave correctly in the cart, and a clean-up of the signals that were quietly
damaging the site.

Part of a two-developer team on the membership programme. The pieces described here
are mine.

## The context

The storefront is a commercial Shopify theme with three different page builders
layered on top of it, plus a cart app and a gift app — the kind of environment where
a change works in isolation and breaks two apps later. Anything added has to survive
that, and has to assume it is not the only thing touching the cart.

## Dental membership

**One source of truth for "is this customer a member right now?"** Membership state
had been read from customer tags, which external systems kept rewriting. A single
snippet now answers the question, and gives a metafield precedence over the tags, so
the rest of the theme stops guessing.

**A cart guard, honest about what it is.** When the host product leaves the cart, the
membership line has to go with it. The guard handles that, keeps the quantity at one,
and survives the race against the cart app and the gift app. It's commented as a
courtesy to the customer, not a trust boundary — enrolment is decided server-side by
a webhook, because anything the browser can do, the browser can also skip.

**Self-service reactivation.** A member who had cancelled had to contact support.
Now they can restart from their account portal — including the case where their
membership can no longer be re-charged, which used to be a dead end.

**Membership looked up by product, not variant.** Retired membership products aren't
published to the Online Store, so a product lookup doesn't find them — which is
exactly what an old cart can still be carrying.

**A QR landing page for in-clinic sign-up**, built to refuse selling a second
membership to someone who already has one.

## Site integrity clean-up

Separate piece of work, on the live theme: removed a hidden third-party backlink and
dead scripts from every layout, then repointed 39 advertising pre-landers and 55
page-builder snippets that were declaring the store as another company's property and
linking their legal pages to a domain that no longer existed.

It's unglamorous work, and it's the kind that quietly costs a store its credibility
with both customers and search engines.

## Stack

Shopify Liquid · Shopify theme architecture · page-builder ecosystems (Replo,
GemPages, Shogun) · cart and subscription apps

## Source code

Private — client work on a licensed commercial theme. Happy to walk through it in a
call.
