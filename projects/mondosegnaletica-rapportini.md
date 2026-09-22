# Mondo Segnaletica — Field Reporting App

Replaces the paper job sheets of a road-signage company. Crews file the day's work
from a tablet at the roadside; the office gets structured data instead of handwriting.

**Live:** [rapp.mondosegnaletica.it](https://rapp.mondosegnaletica.it) (behind login)

## What it does

Crews record what they did street by street — metres of road marking, signs and posts
installed, photos, GPS position, which workers were on site and for how long — on a
tablet, outdoors, often with one hand and no mobile signal. At the end of the day the
foreman sends the report, and the office receives it as a spreadsheet with the photos
attached.

The office side is a separate web application over the same data: crews and sites,
the archive of past reports, totals and exports.

## My role

Sole developer: the data model, both interfaces, the offline layer, the Android
build, the deployment and the handover to the crews.

## Stack

Django · Python · PostgreSQL · HTMX and Alpine.js with no build step · Capacitor
for the Android app

## Engineering highlights

**Offline first, for real.** Roadworks happen where there is no signal. Actions are
queued in the browser's own database, photos included, and replayed in order when
the connection returns. The interface never pretends a save succeeded.

**Safe to retry.** Every action carries an identifier generated on the device and
recorded in the same transaction as the action itself, so a crew tapping twice on a
bad connection files one report, not two.

**A calculation engine that had to agree with the old system.** Nine kinds of work
item, each with its own fields and rules, recalculated server-side in exact decimal
arithmetic — because the totals had to match what the office had been computing for
years.

**Photos shrunk on the device**, from a few megabytes to a few hundred kilobytes,
with no image library, because the upload has to survive a bad connection.

**Worker location handled as a legal question, not a feature.** Tracking is off by
default, limited to working hours, retained for a configurable window and excluded
at the office — Italian labour law sets the boundary, and the code says so.

Around 600 automated tests cover the calculation rules and the offline queue.

## Source code

Private — client work. Happy to walk through the architecture in a call.
