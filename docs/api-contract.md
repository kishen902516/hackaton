# API Contracts — Conversation Intake, Recs & Places

## POST /places/search
Purpose: Find nearby restaurants or groceries that match a recommendation’s facets.

Auth: user JWT (required)  
Rate limit: 20 req/min/user; 2 concurrent searches/session

Request
{
  "rec_id": "UUID | null",
  "rec_facets": ["hydrating","stomach_friendly","cuisine:Chinese","halal"],  // required if rec_id null
  "location": { "lat": 1.3001, "lng": 103.8520 } | null,                     // null -> area_text required
  "area_text": "Raffles Place" | null,
  "radius_km": 1.5,                         // default 1.0 (cap 5.0)
  "filters": {
    "open_now": true,
    "price": ["$", "$$"],
    "delivery": true,
    "veg": false,
    "halal": "strict" | "prefer" | "off"    // strict => show verified only
  },
  "sort": "match" | "distance" | "rating",
  "page_token": "opaque" | null,
  "locale": "en-SG"
}

Response 200
{
  "attribution": ["Foursquare", "Mapbox", "MUIS (verification)"],
  "results": [{
    "id": "plc_4f9c…",
    "provider": "fsq",
    "name": "ABC Congee House",
    "lat": 1.30097, "lng": 103.85275,
    "address": "123 Market St, 01-01",
    "distance_m": 420,
    "rating": 4.3,
    "price_level": "$$",
    "open_now": true,
    "cuisine_tags": ["Chinese","Cantonese"],
    "diet_tags": ["halal_verified"],
    "match_facets": ["hydrating","stomach_friendly","cuisine:Chinese","halal_verified"],
    "actions": {
      "directions_url": "…",
      "order_links": [{"label":"GrabFood","url":"…"}]
    },
    "verification": {
      "muis_certified": true,
      "source_url": "…"
    }
  }],
  "page_token": null,
  "served_in_ms": 780
}

Errors
- 400 invalid_request  – missing location/area_text; bad radius
- 401 unauthorized
- 403 location_permission_required
- 429 rate_limited
- 502 provider_unavailable  – partial results may be included as `"partial": true`
- 500 server_error

Notes
- If `filters.halal = "strict"`, only `diet_tags` containing `halal_verified` are returned.
- Without location, `area_text` geocodes to coarse bbox; user can refine with “Search this area”.

---

## GET /places/{id}
Purpose: Fetch a single place (cached details).

Response 200
{
  "place": { …same shape as in search… },
  "photos": [{ "url": "…", "width": 1024, "height": 768 }]   // if provider allows
}

Errors: 404 not_found, 410 gone (provider deleted)

---

## POST /places/report
Purpose: User reports an inaccurate diet/culture tag.

Request
{ "place_id":"plc_…", "type":"diet_tag_inaccurate", "details":"Not halal", "evidence_url":null }

Response 202
{ "status":"received", "case_id":"rep_…" }

Moderation SLA: < 7 days; repeat offenders → local override list.

---

## GET /places/filters (for UI boot)
Response 200
{
  "cuisines":[ "Chinese","Malay","Indian","Mediterranean","Japanese","Korean" ],
  "price_levels":[ "$","$$","$$$" ],
  "distance_km":[0.5,1,2,5]
}

---

## Provider attribution & display
- Foursquare and Mapbox attribution strings must be shown on Map/List screens.
- MUIS verification badge links to source page.
- If Google Place Details are used for a given place, that view must render on a Google map per licensing (app switches the map layer for that sheet).
