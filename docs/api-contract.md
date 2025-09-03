# API Contracts — Intake, Recs, Places

## POST /intake/turn
Req: { "session_id": "UUID|null", "user_text": "Slept 5 hours, slight headache", "voice_blob": "optional base64", "locale": "en-SG" }
Res: { "session_id":"UUID","system_turn":"How intense is the headache (0–10)?","followups":["0–2","3–6","7–10"],"partial_facts":[{"key":"headache","value":true},{"key":"sleep_h","value":5}] }

## POST /intake/summary
Req: { "session_id":"UUID" }
Res: { "summary": { "facts":[{"key":"hydration_l","value":0.5,"unit":"L","confidence":0.68},{"key":"sleep_h","value":5},{"key":"headache_sev","value":2}], "mood":"low_energy","confidence":0.61 }, "red_flags":[] }

## POST /intake/accept
Req: { "session_id":"UUID", "edits":[{"key":"hydration_l","value":1.0}] }
Res: { "facts_final":[...], "blocked_by_red_flag": false }

## POST /recs/generate
Req: { "facts":[...], "culture":["Malay","Chinese"], "diet_rules":["halal"], "pantry":["eggs","rice"], "time_budget_min":20 }
Res: { "recipes":[{ "id":"rec_...", "title":"...", "time_min":15, "culture":["Chinese"], "diet_tags":["halal_friendly"], "nutrients":{...}, "why":"...", "facets":["steady_energy","cuisine:Chinese","halal"] }] }

## POST /places/search
Req:
{
  "rec_id": "UUID | null",
  "rec_facets": ["hydrating","stomach_friendly","cuisine:Chinese","halal"],
  "location": { "lat": 1.3001, "lng": 103.8520 } | null,
  "area_text": "Raffles Place" | null,
  "radius_km": 1.5,
  "filters": { "open_now": true, "price": ["$","$$"], "delivery": true, "veg": false, "halal": "strict"|"prefer"|"off" },
  "sort": "match"|"distance"|"rating",
  "page_token": null,
  "locale": "en-SG"
}
Res:
{
  "attribution": ["Foursquare","Mapbox","MUIS (verification)"],
  "results": [ { "id":"plc_…","provider":"fsq","name":"ABC Congee House","lat":1.30097,"lng":103.85275,"address":"123 Market St",
    "distance_m":420,"rating":4.3,"price_level":"$$","open_now":true,"cuisine_tags":["Chinese"],"diet_tags":["halal_verified"],
    "match_facets":["hydrating","stomach_friendly","cuisine:Chinese","halal_verified"],
    "actions":{"directions_url":"…","order_links":[{"label":"GrabFood","url":"…"}]},
    "verification":{"muis_certified":true,"source_url":"…"} } ],
  "page_token": null,
  "served_in_ms": 780
}

## GET /places/{id}
Res: { "place": { … }, "photos": [{ "url":"…", "width":1024, "height":768 }] }

## POST /places/report
Req: { "place_id":"plc_…", "type":"diet_tag_inaccurate", "details":"Not halal" }
Res: { "status":"received", "case_id":"rep_…" }

## GET /places/filters
Res: { "cuisines":["Chinese","Malay","Indian","Mediterranean","Japanese","Korean"], "price_levels":["$","$$","$$$"], "distance_km":[0.5,1,2,5] }
