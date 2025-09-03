# UX Flows — “Where to get it” Map

## A) From Recommendations to Map
1. User views RecCards → taps **“Get it near me”** (on a rec) or **Map** tab.
2. If location not granted → LocationPermissionPrompt.
3. MapView loads with pins matched to the selected rec’s facets (e.g., “hydrating, stomach-friendly”).
4. User applies filters (e.g., Halal + Open now).
5. User taps a pin or a list item → PlaceSheet opens.
6. User selects **Directions** → deep link to native Maps; or **Order** → partner app/site.

## B) Manual Location / List-first
1. User denies location → Search bar for area/postcode (e.g., “Raffles Place”).
2. PlaceList populates; user can still open PlaceSheet and act.

## C) Fallbacks
- Place API down → banner + graceful fallback to user-entered search; recs remain available.
- Zero results → suggest clearing filters or increasing distance.

## D) Privacy & Safety
- When location is enabled, show “Using approximate location • Change” chip.
- PlaceSheet always shows diet-tag disclaimer and Report action.
