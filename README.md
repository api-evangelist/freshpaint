# Freshpaint (freshpaint)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Freshpaint is a healthcare privacy platform and customer-data platform that collects first-party event data and governs it for HIPAA compliance before fanning it out to 100+ marketing, analytics, and data destinations. Its server-side HTTP API ingests track, identify, page, and screen events at https://api.perfalytics.com/track authenticated with an environment token.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/freshpaint/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/freshpaint/refs/heads/main/apis.yml)

## Tags

- Customer Data Platform
- Event Tracking
- Healthcare
- HIPAA
- Privacy
- Analytics

## Timestamps

- **Created:** 2026-06-25
- **Modified:** 2026-06-25

## APIs

### Freshpaint Tracking Events API

Server-side HTTP API for sending custom tracked events to Freshpaint via POST /track, authenticated with an environment token in the event payload and routed to all active destinations.

- **Human URL:** [https://documentation.freshpaint.io/reference/developer/http-api](https://documentation.freshpaint.io/reference/developer/http-api)
- **Base URL:** `https://api.perfalytics.com`

#### Tags

- Events
- Tracking
- Server Side

#### Properties

- [Documentation](https://documentation.freshpaint.io/reference/developer/http-api)
- [API Reference](https://documentation.freshpaint.io/integrations/sources/server-side)
- [OpenAPI](openapi/freshpaint-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/freshpaint.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/freshpaint.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Freshpaint Identify API

Server-side identify via the $identify event on POST /track, attaching user properties ($user_props) to a distinct_id to build unified user profiles.

- **Human URL:** [https://documentation.freshpaint.io/reference/developer/http-api](https://documentation.freshpaint.io/reference/developer/http-api)
- **Base URL:** `https://api.perfalytics.com`

#### Tags

- Identify
- User Profiles

#### Properties

- [Documentation](https://documentation.freshpaint.io/reference/developer/http-api)
- [OpenAPI](openapi/freshpaint-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/freshpaint.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/freshpaint.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Freshpaint Page and Screen API

Page and screen events sent through POST /track to trigger virtual pageviews and screen views in downstream destinations, carrying name, category, and contextual properties.

- **Human URL:** [https://documentation.freshpaint.io/reference/developer/freshpaint-sdk-reference](https://documentation.freshpaint.io/reference/developer/freshpaint-sdk-reference)
- **Base URL:** `https://api.perfalytics.com`

#### Tags

- Page
- Screen
- Pageviews

#### Properties

- [Documentation](https://documentation.freshpaint.io/reference/developer/freshpaint-sdk-reference)
- [OpenAPI](openapi/freshpaint-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/freshpaint.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/freshpaint.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Freshpaint Destinations

Destinations are the marketing, analytics, advertising, and data-warehouse tools Freshpaint forwards collected events to. Destinations are configured in the Freshpaint app; per-event routing is controlled with the $options property on the HTTP API. No public REST API for destination configuration is documented.

- **Human URL:** [https://documentation.freshpaint.io/integrations/destinations](https://documentation.freshpaint.io/integrations/destinations)
- **Base URL:** `https://api.perfalytics.com`

#### Tags

- Destinations
- Integrations
- Data Activation

#### Properties

- [Documentation](https://documentation.freshpaint.io/integrations/destinations)

## Common Properties

- [GitHub Organization](https://github.com/freshpaint-io)
- [LinkedIn](https://www.linkedin.com/company/freshpaint)
- [Website](https://www.freshpaint.io)
- [Documentation](https://documentation.freshpaint.io)
- [Plans](plans/freshpaint-plans-pricing.yml)
- [Rate Limits](rate-limits/freshpaint-rate-limits.yml)
- [Fin Ops](finops/freshpaint-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
