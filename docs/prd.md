# PRD v1 — MoodChef (conversation-first + map to get it)

## 1. Goals
- Deliver safe, culture-aware meal & nutrient suggestions tailored by **mood + short conversation**.
- **Help users act now** by showing **nearby places** (restaurants/groceries) to obtain suggested foods, in a **map and list view**.
- Maintain privacy: location is optional, coarse by default, revocable.

## 2. Non-Goals
- Endorsing venues; guaranteeing availability/prices; medical diagnosis/treatment.

## 3. Core Use Cases (MVP)
1) **Daily Check-in (Conversation)** — as defined previously.
2) **Recommendations** — as defined previously.
3) **Where to get it (Map) — NEW**
   - Given recs + culture/diet rules + user location (optional), show a **Map** with pins for:
     - **Ready-to-eat** (restaurants/cafes matching cuisine/diet filters).
     - **Buy ingredients** (groceries/supermarkets that stock key items).
   - Provide **filters**: culture tag, halal/veg, open now, distance, price, delivery/pickup.
   - Each pin → Place sheet: name, rating (if available), hours, distance/ETA, diet/culture tags, quick actions (**Directions**, **Order via partner**, **Save**).
   - Fallback to **list view** if maps disabled; allow manual search by area/postcode.
4) **Weekly Plan & Grocery** — unchanged.
5) **Escalation** — unchanged.

## 4. Functional Requirements (Map & Places)
- **Location & Permissions**
  - Request coarse location by default; support manual location entry.
  - Must function without location (shows list by typed area).
- **Place Matching**
  - For each RecCard, compute **match facets** (e.g., “hydrating beverage,” “magnesium-rich,” “stomach-friendly,” “halal-friendly,” “Chinese cuisine”) and use them to query place providers.
  - Respect **diet rules** (e.g., halal/veg) and **culture preferences** when ranking.
- **Map UX**
  - Map + list toggle; clustering for dense areas; “open now” and “delivery” chips.
  - Tapping a pin opens a **PlaceSheet** with actions and a short rationale (“matches your low-energy plan: protein + complex carbs”).
- **Data & Integrations**
  - Integrate a **maps/places provider** (e.g., major map SDK) and, optionally, food delivery partners.
  - Cache place results for ≤15 minutes; show timestamp “data from partners.”
- **Safety & Disclaimers**
  - Display “External venues; verify menu and allergens with the venue.”
  - Never infer halal status without a reliable tag; allow user report/corrections.

## 5. Non-Functional Requirements
- **Performance**: first map paint ≤ 2s on Wi-Fi; place search ≤ 1.5s warm / ≤ 3.5s cold.
- **Privacy**: store **coarse coordinates** (e.g., 3–4 decimal places) only if user opts in; allow “use once.”
- **Accessibility**: full keyboard navigation for list; map pins reachable via aPlaces list; high-contrast focus states.
- **Resilience**: if place API fails, degrade to local list search and show notice.

## 6. Analytics & Success Criteria
- Map view rate, pin tap rate, directions/order click-through, saved place conversions.
- Per-filter usage (halal/veg/open now).
- Safety: % of user reports about inaccurate diet tags; time to moderation.

## 7. Data Model (adds)
- **places**(id, provider, provider_ref, name, lat, lng, address, cuisine_tags[], diet_tags[], rating, price_level, hours_json, delivery_partners[])
- **place_matches**(rec_id, place_id, match_facets[], score, created_at)
- **user_place_actions**(user_id, place_id, action: "save|directions|order", ts)

## 8. Open Questions
- Which primary maps/places provider at launch? (licensing, SG coverage, halal tagging)
- Do we pull grocery inventory or rely on generic availability + substitutions?
- Delivery deep links vs in-app ordering (later phase).
