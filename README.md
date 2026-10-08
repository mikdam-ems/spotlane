# Spotlane — smart parking finder for Jordan

The Spotlane parking journey on a **real map of Jordan**, built so drivers can test it on their own phones.

| Path | What it is |
|---|---|
| `index.html` | **Landing page**: explains the idea; its search opens the app at that place (`app/?q=…`) |
| `app/` | **Live test version**: real map, car parks, GPS, search and routes |
| `shared/base.css` | Reset and reduced-motion helpers |

Both are plain HTML/CSS/JS with no build step. Serve the folder (for example `python3 -m http.server`) and open it in a browser.

| What's real | What's simulated (clearly labelled in the UI) |
|---|---|
| Map and streets: MapLibre GL + OpenFreeMap tiles | Free spaces and live updates |
| Car parks: OpenStreetMap, via the Overpass API | Prices (except car parks tagged as free) |
| The tester's GPS location, with a demo spot in Amman as fallback | Floors, slots and EV bays |
| Place search: Photon, limited to Jordan | Payment (test mode, no money taken) |
| Driving routes and times: OSRM | Gate opening, parking session, receipt |
| Navigation: hand-off to Google Maps, Waze or Apple Maps | |

All services are free and need no API keys. They're listed in `CONFIG` at the top of the script.

## Share it with testers

Geolocation only works over **https**, so host the repo rather than sending the file:

- **GitHub Pages:** repo → Settings → Pages → Source: *Deploy from a branch* → `main` / root. The landing page is at
  `https://mikdam-ems.github.io/spotlane/` and the app at `/spotlane/app/`. Moderators add `?moderator=1` to the app link.
- **Netlify:** drag the repo folder onto app.netlify.com/drop.

Before sharing, set `CONFIG.feedbackEmail` (top of the script in `app/index.html`) to the address that should receive feedback.
If it's left empty, feedback is copied to the tester's clipboard.

## Running sessions

- **Feedback** (top right of the map) collects:
  - a 1–5 ease rating
  - what the tester was trying to do
  - their comments
  - the tester's steps, such as "hold", "paid" or "nav_handoff"
- The step log never includes location or contact details.
- **Intro cards** show once per browser, on a first visit that didn't come through the landing page. Add `?onboarding=1` to the app link to show them again for the next tester.
- **Location** is only requested when the tester taps "Use my location" (or the locate button). Otherwise the app opens on central Amman.
- **Scenarios** (only shown when the link ends in `?moderator=1`) lets a moderator trigger edge cases on purpose, such as a slot taken at checkout, a declined payment or an expired hold.
- To send events to an analytics tool (PostHog, a Supabase function…), set `CONFIG.analyticsEndpoint`.

## Free-tier limits (fine for testing, not for launch)

- **OSRM demo server and public Overpass:** fair-use services. For a public launch, switch to a hosted provider or self-host.
- **OpenFreeMap:** free, but add your own attribution and monitoring before going public.
