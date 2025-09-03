# PRD v1 — MoodChef (conversation-first + map)

## 1. Goals
- Deliver safe, culture-aware meal & nutrient suggestions tailored by **mood + short conversation**.
- **Time-to-First-Value:** new users get a first useful suggestion in **≤ 5 minutes**.
- Help users act now with **nearby places** (map/list), while preserving privacy.

## 2. Non-Goals
- Diagnosis or treatment guidance; endorsements or guarantees of venue availability; weight-loss coaching; minors.

## 3. Personas
- **Ava, 29, Consultant** — wants quick Asian-leaning ideas when “wired but tired.”
- **Rahim, 34, Engineer** — halal diet; snack swaps for afternoon slumps.
- **Mei, 41, Teacher** — family-friendly Chinese/Malay flavors; low-effort plans.

## 4. Core Use Cases (MVP)
1) **Daily Check-in (Conversation)**
   - 2–4 adaptive questions (hydration, sleep, alcohol, headache presence/severity, triggers, time budget, pantry).
   - System reflects a **plain-language summary** for confirmation/edit.
2) **Recommendations**
   - Given mood + conversation facts + culture/diet rules → 3–5 dishes/snacks with nutrients and “why this helps.”
3) **Where to get it (Map)**
   - Show **Map/List** of nearby **ready-to-eat** (restaurants/cafes) or **buy-ingredients** (groceries) matching facets (culture/diet and rec-specific: hydrating, stomach-friendly, etc.). Filters: open now, distance, price, delivery, halal/veg, cuisine.
4) **Weekly Plan & Grocery**
   - Build 7-day plan from saved items; auto grocery list.
5) **Escalation**
   - Red flags (see §8) → resources/referral; pause suggestions until acknowledged.

## 5. Functional Requirements
### Conversation & Mood
- Adaptive questions; max 4 by default (6 if confidence low); **skip** and **manual entry** always available.
- Optional mood estimate via **face (landmarks)** and **voice (prosody)** with per-device consent; **not identity recognition**.
- Output a **structured summary** (facts + mood + confidence); editable inline.

### Recommendations (intake-aware)
- Headache mild (≤3/10) → hydration + magnesium/riboflavin-forward; avoid known triggers unless user overrides.
- Hangover-likely (alcohol last night) → rehydration/electrolytes; gentle carbs/protein; stomach-friendly options.
- Fatigue cues → steady-energy (complex carbs + protein; iron/B12 sources); caffeine guidance.
- Each RecCard shows: dish title, image, time, macros + 2–3 key micros, why-this, culture/diet badges, substitutions.

### Map & Places
- Request **coarse location** by default; manual area entry supported.
- Place match facets derived from RecCard + user profile; rank by match, distance, rating, open now, price.
- PlaceSheet: name, rating, distance/ETA, hours, diet/culture badges, “Why it matches,” **Directions/Order/Save**, attribution, allergen disclaimer.
- **Halal behavior:** `strict` (verified only) / `prefer` (verified first) / `off` — user-controllable.
- Data freshness: cache places ≤ 15 min; show “data from partners” note.

### Onboarding & First-Run (TTFV guardrail)
- Only essential steps pre-first rec: disclaimer & consent → culture/diet quick pick (skippable) → optional cam/mic (skippable) → 2–4 question conversation.
- If on-device model download exceeds budget, auto-route to conversation-only path.

## 6. Non-Functional Requirements
- **Performance**
  - Conversation turn: ≤ 1.5s warm / ≤ 4s cold.
  - Recommendations: ≤ 2s warm / ≤ 6s cold.
  - First map paint: ≤ 2s on Wi-Fi.
- **TTFV**
  - Definition: first launch → first RecCard rendered.
  - Targets: median ≤ 3 min; P90 ≤ 4 min; **P95 ≤ 5 min** (release gate).
- **Availability**: 99.5% MVP; degrade gracefully (manual intake if ML down; list-only if map down).
- **Accessibility**: WCAG 2.2 AA; keyboard-only & captions.
- **Privacy**: no raw A/V stored; derived facts only; consent per device; location optional/coarse.

## 7. Data Model (top-level)
- User, Profile (culture/diet rules), ConsentRecord, ConversationSession, IntakeFact, MoodCheck, Recipe, NutrientProfile, Recommendation, Plan, Feedback, EscalationEvent, Place, PlaceMatch, UserPlaceAction.

## 8. Safety & Red Flags (trigger escalation)
- Headache severity ≥7, “worst ever,” sudden onset, fever, vision/neurological symptoms, repeated vomiting, chest pain, suicidal ideation, pregnancy concerns.
- Alcohol: blackouts, severe vomiting, confusion.
- Action: show resources & defers suggestions until acknowledged; audit entry.

## 9. Analytics & Success Criteria
- Events: `first_launch`, `onboarding_step`, `conversation_started`, `first_rec_shown`, `map_view_opened`, `filter_applied`, `pin_opened`, `directions_clicked`, `order_clicked`.
- KPIs: TTFV median ≤ 3m / P95 ≤ 5m; Map view ≥ 30%; Place CTR ≥ 10%; Safety FP < 1%.

## 10. Open Questions
- Primary maps/places & halal verification method (MUIS import vs manual link).
- Nutrition providers final pick and locale coverage depth.
