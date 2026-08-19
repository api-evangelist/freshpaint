---
name: Identify a user and emit page/screen events server-side
description: >-
  Use the reserved $identify, $page and $screen event names on the Freshpaint
  HTTP Events API to attach user profile properties and record page and screen
  views from a backend, keeping server-side activity stitched to the same user
  as the browser and mobile SDKs.
api: openapi/freshpaint-events-api-openapi.yml
operations: [track]
generated: '2026-08-13'
method: generated
source: >-
  openapi/freshpaint-events-api-openapi.yml (request examples for the
  $identify, $page and $screen variants) plus
  conventions/freshpaint-conventions.yml and
  data-model/freshpaint-data-model.yml. The operationId `track` was verified
  against the spec.
---

# Identify a user and emit page/screen events server-side

Freshpaint has no separate `/identify` or `/page` endpoint. All three are the
same operation — `track` (`POST /track` on `https://api.perfalytics.com`) —
switched by a **reserved value** in the `event` field.

| `event` value | Behavior |
|---|---|
| `$identify` | Attach `$user_props` to the profile keyed by `distinct_id` |
| `$page` | Page view |
| `$screen` | Mobile screen view |
| any other string | Custom tracked event |

This is a value-based variant, not an OpenAPI discriminator. The spec declares
one schema; the behavior difference lives in the description and the request
examples.

## Identify

```json
{
  "event": "$identify",
  "properties": {
    "distinct_id": "user@example.com",
    "token": "<environment id>",
    "time": 1719446400,
    "$user_props": { "plan": "pro", "company": "Acme" }
  }
}
```

Rules:

- `$user_props` is the profile bag. It is an open object — any keys you send
  become user properties. It is meaningful **only** on `$identify`.
- `distinct_id` is the profile key. Use the same value the browser and mobile
  SDKs pass to `freshpaint.identify()`, or you will create a second profile
  and split the user's history.
- Identify before, or in the same batch as, the events you want attributed —
  properties set later do not retroactively re-attribute earlier events at
  every destination.
- Send `$identify` only when the profile actually changed. Every call is a
  billable event and fans out to destinations.

## Page and screen

```json
{
  "event": "$page",
  "properties": {
    "distinct_id": "user@example.com",
    "token": "<environment id>",
    "time": 1719446400,
    "name": "Pricing"
  }
}
```

Use `$screen` instead of `$page` for native mobile screens. Page and screen
events carry the same required fields as any other event; the page or screen
name rides in `properties` as an ordinary custom property.

Server-side `$page` is for backends that render pages themselves. If the
browser SDK is already loaded on the page, it emits `$page` automatically —
sending it again from the server double-counts.

## Identity stitching

`distinct_id` is the join key across every surface. `$device_id` is the
secondary key used for stitching and deduplication and is usually only
available client-side. When a server-side event has no `$device_id`, set
`$insert_id` explicitly (see the `freshpaint-send-server-side-event` skill) —
otherwise the implicit deduplication key degrades to `time` alone.

## Overriding captured context

- `$ip` overrides the source IP Freshpaint would otherwise capture. Set it when
  proxying a client request through your backend, or every event will be
  attributed to your server's geography.
- `$options` restricts which destinations receive the event. Reserve it for
  events that must not reach a given destination for compliance reasons.

## Errors

Same three declared statuses as any `track` call: `200` accepted, `400`
malformed or missing required properties, `429` rate limited (5000 req/s
burst). No response body schema is published, and no authentication-failure
status is declared — confirm in the Freshpaint app that identifies are landing
rather than trusting a `200`.
