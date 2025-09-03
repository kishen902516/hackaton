# Sprint: MVP Places & Map (Target: 2 weeks)

## BE — Providers & Search
1. BE-PL-001: Foursquare adapter (category, cuisine, halal cat, keyword)
   - AC: Query by bbox + keyword; map FSQ fields to PlaceResult; retries+timeout 300ms
   - Est: 6 pts
2. BE-PL-002: Mapbox geocoding & “Search this area” bbox support
   - AC: area_text→bbox; map/list re-query by bbox; error states
   - Est: 3 pts
3. BE-PL-003: Aggregator & ranking service
   - AC: Merge+dedupe (name+geo hash); apply config/places-ranking.yaml; paging
   - Est: 8 pts
4. BE-PL-004: MUIS verification lookup
   - AC: Nightly cache; fuzzy match; attach `verification.muis_certified` + source URL
   - Est: 5 pts
5. BE-PL-005: `/places/search`, `/places/{id}`, `/places/report` endpoints
   - AC: Auth, rate limits, telemetry, attribution plumbing
   - Est: 5 pts
6. BE-PL-006: Google Details enrich (optional, sheet-only)
   - AC: Conditional fetch; switch to Google map layer on sheet
   - Est: 3 pts

## FE — Map, List, Sheet
7. FE-PL-101: MapView + List toggle
   - AC: Map/list parity; clusters; “Search this area”; SSR-safe shell
   - Est: 8 pts
8. FE-PL-102: FiltersBar (Open now, Halal, Veg, Distance, Price, Cuisine)
   - AC: Persist in URL state; keyboard accessible
   - Est: 5 pts
9. FE-PL-103: PlaceList (a11y-first)
   - AC: Full keyboard nav; SR-friendly; sorts; pin mirror
   - Est: 5 pts
10. FE-PL-104: PlaceSheet
    - AC: Badges, “Why it matches”, Directions/Order/Save, attribution & disclaimer
    - Est: 5 pts
11. FE-PL-105: LocationPermissionPrompt + manual area entry
    - AC: “Use once”, “Allow always”, manual area; copy deck hooks
    - Est: 3 pts

## Shared / QA / Analytics
12. QA-PL-201: Provider outage & zero-results scenarios
    - AC: Fallback banners; list-only mode; tests
    - Est: 3 pts
13. AN-PL-301: Analytics events & dashboards
    - AC: `map_view_opened`, `filter_applied`, `pin_opened`, `directions_clicked`, `order_clicked`
    - Est: 2 pts
14. SEC-PL-401: Location privacy checks
    - AC: Coarse coord storage toggle; “Use once”; revoke flow; audit
    - Est: 3 pts

**Total** ≈ 60 pts

Dependencies
- API keys (FSQ, Mapbox; optional Google)
- MUIS data access method (scrape-to-cache or manual import)
- Copy deck for disclaimers & permissions

Definition of Done
- Map & List render matching places for at least one rec facet set in SG CBD
- Halal strict/prefer/off behaviors verified
- MUIS badge appears when matched
- Analytics events visible in dashboard
- A11y audit passes WCAG 2.2 AA on Map/List/Sheet flows
