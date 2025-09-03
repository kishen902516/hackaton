# Project Brief — “MoodChef”
One-line vision  
> An AI mood chef + health advisor that turns your face/voice signals, culture, and context into safe, tasty meal & nutrient suggestions — with pro referrals when needed — and shows nearby places to get the recommended food on a map.

## Target users
- Wellness-minded adults who want food guidance tied to how they feel (stress, low energy, mood swings).
- Busy professionals & students seeking quick, culturally familiar meal ideas and nearby options.
- People exploring nutrition for general wellbeing (not acute care).

## Problem
- Generic diet tips ignore mood, culture, daily context, and common day-to-day ailments (fatigue, headache, hangover).
- Users don’t know which nutrients/foods map to their current state or where to conveniently get them.

## Solution
- Consent-based face + voice read to estimate mood/energy range (on-device when possible), with a **short conversational intake** (2–4 natural questions; adaptive; manual override).
- Recommendations: meals, snacks, beverages, and micronutrients with rationale and credible sources; **symptom-aware variants** (hydration-forward for hangover; magnesium/complex carbs for fatigue) and **clear non-medical guidance**.
- **Place Finder + Map:** show nearby restaurants/cafes/groceries that match culture/diet rules (e.g., halal/veg) and the current recommendation; map filters (open now, price, distance, delivery/pickup); deep links to directions/delivery.
- Cultural preference engine (Indian, Malay, Chinese, Mediterranean, etc.) + dietary rules (halal/vegetarian, allergies).
- Integrations for nutrition facts, place search, and pro advice/telehealth triage.
- Clear guardrails: not diagnostic; escalate to clinician when red flags appear.

## Differentiators
- Multimodal mood + **conversation-driven intake** (no dropdowns).
- **Culture- and venue-aware** recs with a map to act now.
- Safety by design: privacy, explainability, escalation rules.

## Supported everyday patterns (via conversation)
- **Fatigue (low energy)**, **Headache (non-severe)**, **Hangover (post-alcohol)** — tailored foods and **nearby sources**.

> **Safety note:** Severe/atypical symptoms (e.g., “worst headache”, fever, neuro signs, repeated vomiting, chest pain) trigger escalation and pro resources. Wellness only; not diagnostic.

## Success metrics (MVP → 90 days)
- D1 conversation completion ≥ 60%
- ≥ 3 recs saved/week/user
- **≥ 30% sessions view map or tap a place**
- **≥ 10% place click-through to directions/order**
- ≥ 25% users set culture/diet profile
- < 1% escalation false-positives; zero PII incidents

## Risks & mitigations
- **Biometric bias/inaccuracy** → user confirmation; confidence shown; manual override.  
- **Privacy** → opt-in biometrics; data minimization; local processing; PDPA/GDPR.  
- **Medical safety** → wellness scope; escalation rules; vetted sources.  
- **Place data quality** → multiple sources; verification badges; user reports.

## Scope (MVP)
- Daily check-in (mood) + conversational intake; culture/diet profile; **map-backed place suggestions**; 3–5 dish ideas with nutrients & rationale; grocery list; weekly plan; escalation.

## Out of scope
- Medical diagnosis/treatment; endorsements/availability guarantees; minors’ nutrition.
