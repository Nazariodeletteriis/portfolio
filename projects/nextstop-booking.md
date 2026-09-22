# Next Stop Parking — Airport Valet Booking

A WordPress booking plugin written from scratch for an airport parking and valet
service: the customer books a service and a time slot, the operator sees the day.

## What it does

The business sells time-based services — guarded parking, valet handover, shuttle,
car wash — that a generic contact form can't take a booking for. It needs dates and
times, vehicle details, a price and a confirmation the customer can show on arrival.

The plugin handles the whole flow: a five-step booking form, a booking record with
its own reference code, confirmation emails to both customer and operator, and an
admin side with a table and a month calendar colour-coded by service.

## My role

Sole developer of the plugin. The site around it runs on a commercial theme; the
booking system is mine.

## Stack

PHP · WordPress · MySQL with custom tables · jQuery and vanilla JS · SMTP delivery

## Engineering highlights

**A five-step form that survives a closed tab.** The booking in progress is kept in
the browser, validated step by step, with a desktop stepper and a separate mobile
layout with a persistent action bar — most of these bookings happen on a phone, in a
hurry, before a flight.

**Server-side submission done properly.** The booking endpoint verifies a nonce,
sanitises every field individually, validates the time format, and enforces the rule
that a time-based service can't be booked without dates and times.

**Its own data, not a pile of post meta.** Bookings live in dedicated tables created
on activation, with a non-public custom post type for the admin views and custom
columns so the operator reads a booking at a glance.

**A month calendar for the operator**, events coloured per service, with a detail
popup — because the real question is never "show me booking #481", it's "what does
Tuesday look like".

**Email configured for deliverability**, with SMTP settings and a forced sender, each
option sanitised through its own callback.

## Status

In production. The pricing calculation currently runs client-side — moving it to the
server is the next piece of work.

## Source code

Private — client work. Happy to walk through it in a call.
