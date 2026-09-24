# StackFit Web

Create workouts, log sets, and run Tabata-style timers in the browser. Works on a phone and a computer. Data stays on the device.

Live files: open `index.html` or enable GitHub Pages on this repo (`Settings → Pages → Deploy from branch → main`).

After Pages is on, the app is at:

https://kuikai.github.io/stackfit-web/

## Why this exists

The Flutter StackFit app was a timer-first prototype. This is the missing half: a **web logbook** you can build on a desk and run in the gym.

Same loop as Hevy / Strong, without the account:

1. Save a template (Push Day, Tabata bodyweight, …)
2. Start it and log weight × reps. Last time’s numbers sit in grey.
3. Rest timer starts when you tick a set.
4. Or open Timer and run 20/10 × 8 without a template.

## Stack

Vanilla HTML, CSS, JavaScript. No build step. `localStorage` for workouts, sessions, and settings. Optional service worker for offline after the first visit.

## Open locally

Any static server from this folder:

```bash
python3 -m http.server 4173
```

Then http://localhost:4173

## Spec

See [ACCEPTANCE_CRITERIA.md](./ACCEPTANCE_CRITERIA.md).
