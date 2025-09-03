# Component Spec — Conversation Intake + “Where to get it” Map

## Existing (context)
- ChatPane, PromptChips, SummaryCard, EscalationModal, RecCard, PrivacyCenter (unchanged basics).

## NEW — Map & Places

### 1) MapView
Purpose: Show nearby venues to obtain a selected recommendation (ready-to-eat or buy-ingredients).

Props
- `center: {lat,lng}|null`  // null → fit to results or typed area
- `results: PlaceResult[]`   // clustered if dense
- `userLocation: {lat,lng}|null`
- `filters: MapFilters`      // openNow, price, distanceKm, halal, veg, cultureTags[], delivery
- `mode: "map"|"list"`
- `selectedRec: RecSummary`  // used to form match facets/badges
- `onPinClick(placeId)`, `onListItemClick(placeId)`, `onRequestDirections(placeId)`

States
- loading, empty, error, location-permission-blocked

Interactions
- Pin tap/click → opens PlaceSheet
- Drag/zoom map → “Search this area” chip appears
- Toggle map/list
- Cluster tap → zoom into cluster
- “Open now” / “Delivery” chips toggle without full page reload

Accessibility
- Every pin mirrored as a **ListItem** in PlaceList; keyboard can reach and open it
- Screen reader: announce “{name}, {distance}, {cuisine}, {diet badges}, {open/closed}”

Analytics
- `map_view_opened`, `pin_opened`, `search_this_area_clicked`, `filter_applied`

### 2) PlaceList
Purpose: Accessible, scrollable list view of results (map-independent).

Props
- `results: PlaceResult[]`, `sortBy: "match"|"distance"|"rating"`

Cells show
- Name, rating (if present), distance/ETA, price level
- Diet & culture badges (e.g., halal, veg, Chinese)
- “Directions”, “Order”, “Save” quick actions

Accessibility
- Full keyboard operable; list acts as the source of truth for SR users

### 3) FiltersBar
Purpose: Fast refinement.

Controls
- Chips: **Open now**, **Delivery**, **Halal**, **Vegetarian**
- Dropdowns: **Distance** (0.5–10 km), **Price** ($–$$$), **Cuisine/Culture**
- Sticky at top in list mode; floating in map mode

### 4) MapListToggle
Purpose: Switch between map and list layouts.
- Mobile: segmented control in header; Desktop: right-aligned pill toggle

### 5) PlacePin
Purpose: Visual marker with match score halo (optional).
- Variants: restaurant, grocery
- Badge overlays when a strong match to the selected Rec (e.g., “Hydrating”, “Stomach-friendly”)

### 6) PlaceSheet
Purpose: Rich details and actions for a place.

Props
- `place: { id, name, lat, lng, address, rating?, priceLevel?, hours[], phone?, url?, deliveryPartners[], dietTags[], cuisineTags[], evidence?: MatchFacet[] }`
- `recContext: RecSummary`  // used to show “Why this matches”
- Handlers: `onDirections()`, `onOrder(partner)`, `onSave()`, `onReportIssue()`

Layout
- Header: name, rating, price, distance/ETA
- Badges: diet (halal/veg), culture/cuisine
- “Why it matches”: short rationale using rec facets (e.g., “Offers electrolyte beverages; stomach-friendly soups”)
- Actions: **Directions**, **Order** (deep link), **Save**
- Disclosure: “External venue; verify allergens with venue.”
- Footer: hours (localized), address, phone/open in maps

Empty/Edge
- Unknown diet tag → show “Unverified” with tooltip and Report button

Accessibility
- Trap focus inside sheet; ESC to close; all actions have accessible names

Analytics
- `place_sheet_opened`, `directions_clicked`, `order_clicked`, `place_saved`, `diet_tag_reported`

### 7) LocationPermissionPrompt
Purpose: Progressive ask for location.

Variants
- **Coarse first** (“Use approximate location”) with “Use once” option
- **Manual location entry** (search bar) when denied

Copy (short)
- Title: “See nearby options?”
- Body: “Use your approximate location to show places. You can change this anytime.”

### 8) NoResults / Error States
- NoResults: “No places match these filters here. Try a wider distance or switch to list.”
- Error: “We can’t load places right now. Your food suggestions still work.”
