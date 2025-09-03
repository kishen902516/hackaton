# Project Brief — “MoodChef”
One-line vision  
> An AI mood chef + health advisor that turns your face/voice signals, culture, and context into safe, tasty meal & nutrient suggestions — with pro referrals when needed — **and shows nearby places to get the recommended food on a map**.

## Target users
- Wellness-minded adults who want food guidance tied to how they feel (stress, low energy, mood swings).
- Busy professionals & students seeking quick, culturally familiar meal ideas **and nearby options**.
- People exploring nutrition for general wellbeing (not acute care).

## Problem
- Generic diet tips ignore mood, culture, daily context, and common day-to-day ailments (fatigue, headache, hangover).
- Users don’t know which nutrients/foods map to their current state **or where to conveniently get them**.

## Solution
- Consent-based face + voice read to estimate mood/energy range (on-device when possible) with a **short conversational intake** (no dropdowns).
- Recommendations: meals, snacks, beverages, and micronutrients with rationale and credible sources; symptom-aware variants (hydration-forward for hangover; magnesium/complex carbs for fatigue).  
- **Place Finder + Map:** for each recommendation, suggest **nearby restaurants, cafes, or grocery stores** that match culture/diet rules (e.g., halal/veg) and ingredients. Show on a **map with filters** (open now, price, distance, delivery/pickup). Deep link to directions or delivery apps.
- Cultural preference engine (e.g., Indian, Malay, Chinese, Mediterranean, etc.) + dietary rules (halal/vegetarian, allergies).
- Integrations for nutrition facts, place search, and pro advice/telehealth triage.
- Clear guardrails: not diagnostic; escalate to clinician when signals/answers cross thresholds.

## Differentiators
- Multimodal mood + **conversation-driven intake**.
- **Culture- and venue-aware** recs (restaurants or groceries) with map view.
- Safety by design: privacy, explainability, escalation rules.

## Supported everyday patterns (MVP) — via conversation
- **Fatigue (low energy)**, **Headache (non-severe)**, **Hangover (post-alcohol)** with tailored foods and **nearby sources**.

> **Safety note:** Severe or atypical symptoms trigger escalation prompts and pro resources. General wellness only.

## Success metrics (MVP → 90 days)
- D1 conversation completion ≥ 60%
- ≥ 3 recs saved/week/user
- **≥ 30% of sessions view the Map or tap a Place**
- **≥ 10% place click-through to directions/order**
- ≥ 25% users set culture & dietary profile
- < 1% escalation false-positives (reviewed), zero PII incidents

## Risks & mitigations
- **Place data quality/coverage** → multiple data sources; clear “data from partners” labeling; user feedback.
- **Location privacy** → explicit opt-in; **coarse location** by default; on-device geofencing; easy revoke.
- **Medical safety & bias** → as previously defined; no cure/diagnosis claims.

## Scope (MVP)
- Daily check-in (mood) + conversational intake; culture/diet profile; **map-backed place suggestions** for eat-out or buy-ingredients; 3–5 dish ideas with nutrients & rationale; grocery list; weekly plan; escalation.

## Out of scope (MVP)
- Real-time indoor availability; delivery guarantees; endorsements of specific providers.
