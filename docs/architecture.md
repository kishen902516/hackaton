# Architecture — Modular Monolith + ML sidecar

## Stack
- **Frontend**: Next.js (App Router), TypeScript, WebRTC capture, Map layer (Mapbox; Google layer on sheet when using Google Details).
- **Backend**: NestJS, PostgreSQL, Redis (cache/queues), S3-compatible object storage.
- **ML sidecar**: FastAPI (Python) for mood inference; optional on-device WASM for face landmarks; voice prosody via WebAudio.
- **Integrations**: Nutrition (Edamam + USDA FDC), Places (Foursquare + Mapbox; optional Google Details), MUIS verification overlay.

## Modules
- **api-gateway**: `/auth/*`, `/consent/*`, `/intake/*`, `/recs/*`, `/places/*`, `/plans/*`, `/grocery/*`, `/privacy/*`
- **conversation-orchestrator**: adaptive Q&A; emits IntakeFacts; summary; red-flag checks.
- **ml-mood**: `/infer` (facial keypoints & voice features) returning mood + confidence.
- **recommender**: hybrid rules+retrieval using profile, facts, culture/diet; caches recs.
- **places-aggregator**: provider fan-out + ranking; MUIS verification; attribution.
- **safety-engine**: red-flag detection & blocking.
- **privacy-center**: DSR flows; audit logs; data residency.

## Data
- Tables as per PRD §7; object storage for images; no raw A/V persisted; ephemeral buffers only.

## Deployment & Observability
- Containers; managed Postgres; CDN; logs/traces/metrics; privacy audit trails; provider timeouts & alarms.
