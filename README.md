# Freshpaint (freshpaint)

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
