# Provider Setup Checklist
- Decisions: providers; halal default; launch geos/radius.
- Accounts/keys: Foursquare, Mapbox, (Google optional), Edamam, USDA FDC, (Nutritionix optional), MUIS method.
- Legal/ToS & branding; attribution strings in UI.
- Security: key restrictions/rotation; secrets manager; CI secret scan.
- Env templates (.env & providers.json); feature flags; timeouts.
- Implementation gates: /places/*, Map/List/Sheet; MUIS cache; analytics.
- Quotas/monitoring; QA & a11y; launch readiness; rollout plan.
