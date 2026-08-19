---
name: Send a server-side event to Freshpaint
description: >-
  Emit a custom tracked event from a backend to the Freshpaint HTTP Events API
  so it fans out to the account's active destinations, with correct
  authentication, deduplication on retry, and rate-limit handling.
api: openapi/freshpaint-events-api-openapi.yml
operations: [track]
generated: '2026-08-13'
method: generated
source: >-
  openapi/freshpaint-events-api-openapi.yml plus
  conventions/freshpaint-conventions.yml, errors/freshpaint-problem-types.yml
  and rate-limits/freshpaint-rate-limits.yml. Every operationId used here was
  verified against the spec.
---

# Send a server-side event to Freshpaint

Freshpaint's entire public API is one operation: `track` — `POST /track` on
`https://api.perfalytics.com`. Everything else (destinations, consent rules,
audiences) is configured in the Freshpaint app and has no public REST API. Do
not attempt other paths.

## Before you start

Get the **environment ID** from the Server Side API section of the Sources page
in the Freshpaint app. This value is both the tenancy key and the credential.

## Authentication — read this carefully

The credential does **not** go in a header or a query string. It goes inside
the JSON body as `properties.token`.

Consequences you must respect:

- Never log the request body. The credential is in it.
- Never put the token in the URL, even though the OpenAPI models the scheme as
  `apiKey`/`in: query`. That modeling is an OpenAPI 3.0 limitation, not the
  wire format.
- One token addresses one environment. Sending a production event with a
  development token silently routes it to the wrong environment's destinations.

## Steps

1. **Build the envelope.** Call `track` with a body matching
   `#/components/schemas/Event`:

   ```json
   {
     "event": "Order Completed",
     "properties": {
       "distinct_id": "user@example.com",
       "token": "<environment id>",
       "time": 1719446400,
       "$insert_id": "<your own stable id for this event>",
       "revenue": 49.99
     }
   }
   ```

   Required: top-level `event` and `properties`; inside `properties`,
   `distinct_id`, `token` and `time`. `time` is **epoch seconds**, an integer —
   not milliseconds and not ISO 8601.

2. **Name the event.** Any string is a custom tracked event. Four names are
   reserved and change the meaning of the envelope: `$identify`, `$page`,
   `$screen`. Do not use a reserved name for a custom event.

3. **Set `distinct_id` to the same identifier you use client-side.** It is
   usually an email address, and it must match what `freshpaint.identify()`
   passes from the browser or mobile SDK, or the server-side and client-side
   activity will not stitch into one user.

4. **Always set `$insert_id` yourself.** This is the deduplication key. If you
   omit it, Freshpaint computes one from `time` and `$device_id`, which is
   fragile for server-side events that often have no device id. Derive it from
   something stable in your domain (the order id, the job id) so a retry
   produces the same value.

5. **Restrict routing when the event is sensitive.** `properties.$options`
   takes either an allow-list of destinations the event may reach or a
   deny-list of destinations it must be withheld from. In a HIPAA context this
   is the per-event control — use it rather than assuming account-level
   configuration is sufficient.

6. **Send one event per request.** The contract declares a single `Event`
   object as the request body, not an array. There is no documented batch
   endpoint.

## Handling the response

The contract declares three statuses and no response body schema. You get a
status code and nothing else to act on.

| Status | Meaning | What to do |
|---|---|---|
| 200 | Accepted for ingestion | Done. 200 means accepted, not delivered — it says nothing about whether destinations received it. |
| 400 | Malformed payload or missing required properties | Do not retry as-is. Validate `event`, `properties.distinct_id`, `properties.token`, `properties.time`. |
| 429 | Rate limited | Back off and retry with the **same** `$insert_id`. |

Nothing else is declared — including no `401`/`403`. The contract does not say
what an invalid or missing environment token returns, so **do not treat a 200
as proof the token was valid.** Verify in the Freshpaint app that events are
arriving before trusting a new integration.

## Rate limits

The documented burst limit is **5000 requests/second** on `POST /track`, and
exhaustion returns `429`. There are no `RateLimit-*` or `X-RateLimit-*` headers
and no `Retry-After`, so you cannot read remaining budget from a response.
Choose your own backoff — exponential with jitter — and rely on `$insert_id`
to make retries safe.

## Do not

- Do not send PHI in event properties beyond what the account's Freshpaint
  configuration is set up to govern. Freshpaint's value is filtering sensitive
  data before it reaches destinations, but that filtering is configured in the
  app, not inferred from the payload.
- Do not invent endpoints. `POST /track` is the only public operation.
- Do not retry a `400`.
