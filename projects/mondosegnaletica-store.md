# Mondo Segnaletica — B2B Road Signage Store

WooCommerce store for a road-signage manufacturer: 1,200 products and 35,000
variants, taken from a supplier's PDF price list and turned into a catalogue people
can actually search.

## What it does

Road signs are sold by type, size and reflective class, priced ex-VAT, and a good
part of the catalogue has no list price at all — those need a quote. None of that
fits a standard shop.

The store handles it: a custom theme built from scratch on WooCommerce, quote
requests where a price doesn't exist, B2B fields at checkout, and a catalogue
imported from the supplier's printed price lists.

## My role

Sole developer: the theme, the WooCommerce work, the import toolchain and the
front-end build.

## Stack

PHP 8.1 · WordPress · WooCommerce (HPOS-compatible) · custom theme · Vite 5 +
Tailwind · Python 3 for the data pipeline · WP-CLI

## Engineering highlights

**The build refuses a design token that doesn't exist.** A check runs before every
build and compares every CSS variable used against the ones declared. It exists
because a missing token once shipped to production and silently removed the spacing
of a whole layout: the browser doesn't complain, the page just looks wrong.

**Getting a paper catalogue into a database.** PDF price lists are extracted,
normalised and imported through WP-CLI with a dry-run mode. Products without a list
price are created without one, so WooCommerce itself marks them unpurchasable and
the theme shows a quote request instead.

**Matching product photos by reading them.** The images in the price lists don't
line up with the rows positionally — matching them that way was wrong 9% of the time
and dropped fourteen pages entirely. OCR reads the figure code and the text printed
on the sign itself, and the assignment is solved on both signals. Correct images went
from around 300 to 610.

**A scraper that stops where the data stops.** Supplier images are matched by figure
code only, never by fuzzy name, at one request per second. Coverage is measured and
reported honestly: 143 of 146, not more.

**Forms without a plugin.** Nonce, honeypot, timing check and rate limiting, with
post-redirect-get so a refresh doesn't send the message twice.

## Status

In development — the storefront is being finished, the landing page is live.

## Source code

Private — client work. Happy to walk through the architecture in a call.
