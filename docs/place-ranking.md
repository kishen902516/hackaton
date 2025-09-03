version: 1
weights:
  facet_match: 0.45
  distance: 0.25
  rating: 0.15
  open_now: 0.10
  price_fit: 0.05

distance_buckets:          # score contribution before weight
  - { max_m: 500, score: 1.0 }
  - { max_m: 1000, score: 0.8 }
  - { max_m: 2000, score: 0.6 }
  - { max_m: 5000, score: 0.3 }
  - { max_m: 999999, score: 0.1 }

facet_rules:
  base:
    halal_verified: 0.25         # applied if required or matched
    halal_preferred: 0.15
    culture_match: 0.10          # cuisine tag matches user culture
    stomach_friendly: 0.08
    hydrating: 0.08
    electrolyte: 0.08
    veg: 0.10                     # when user diet_rules include veg
  clamps:
    muis_verified_min_score: 0.7  # clamp final score to >= this
  penalties:
    unverified_halal_when_strict: -1.0  # filtered out

rating_normalization:
  min: 3.5
  max: 5.0

price_fit:
  match: 1.0
  near: 0.7
  far: 0.3

provider_timeouts_ms:
  fsq: 300
  mapbox: 300
  google_details: 500

cache:
  ttl_minutes: 15
  vary_by: ["rec_facets_hash","bbox_hash","filters_hash"]

verification:
  muis_match_strategy:
    keys: ["normalized_name","postal_code"]
    fuzzy_threshold: 0.88
  tags:
    verified_halal: ["muis_certified", "provider_attr:halal_certified"]
    unverified_halal: ["user_tag:halal","keyword:halal"]
