# Spotlane — working conventions

A smart parking finder for Jordan, currently in the **user-testing stage** (Stage 1).

## Layout
- `index.html` — landing page: explains the idea and hands a search to the app as `app/?q=<place>`.
- `app/index.html` — live test build. MapLibre + OpenFreeMap tiles, OpenStreetMap car parks via Overpass, Photon search, OSRM routes, and hand-off to Google Maps / Waze / Apple Maps. All external services are listed in `CONFIG` at the top of the script.
- `shared/base.css` — reset and reduced-motion helpers.

## Rules
- No build step. Libraries come from CDNs only (unpkg / jsdelivr / cdnjs).
- Anything simulated (availability, prices, slots, payment, gate) must stay labelled as simulated in the UI.
- Responsive down to 360px, a `prefers-reduced-motion` fallback, and no horizontal scroll.
- Currency is JD. Plates default to JO. Arabic / RTL support is planned.
- The test log (`track()`) must never record coordinates or contact details.
- Verify changes in headless Chromium (desktop and mobile) before pushing.

## Roadmap
1. Stage 1: moderated user tests with this build. Next: test script, Arabic RTL, installable PWA.
2. Stage 2: concierge pilot with 2–3 garages. Operator page, Supabase backend, phone sign-in with a one-time code, pay at the gate.
3. Stage 3: MVP with a Jordanian payment provider, garage gate integration, and an operator portal.
