# StackFit Web — Acceptance Criteria (MVP)

**Product:** StackFit Web  
**Repo:** https://github.com/kuikai/stackfit-web  
**Platform:** Responsive web app (phone + desktop). Offline-first. No account.  
**Style:** Clean, minimal, dark-first. Fast to log. One job: plan a workout, run it, keep the numbers.

---

## Coherence check (why these features belong together)

The original ask is three jobs that already share a data model:

1. **Create a workout** — a reusable template of exercises.
2. **Log a workout** — fill weight × reps (or time) against that template, then keep the session.
3. **Timer** — Tabata / intervals with work, rest, and rounds.

They fit if we treat them as one loop, not three apps:

```
Template  →  Start session  →  Log sets + rest timer  →  Save history
                ↘
             Standalone interval timer (Tabata etc.) can also write a history session
```

A template without logging is a recipe book. Logging without templates means rebuilding the same day every visit. A timer without history is a kitchen clock. Together they are a training log you can use at a desk (build the week) and on a phone (run the session).

What we deliberately do **not** add in MVP: social feed, AI programming, video demos, accounts/cloud, subscriptions. Those fight the “open it and train” job.

---

## 1. First launch & layout

- [x] App loads with no login.
- [x] Desktop: left sidebar + wide main column.
- [x] Phone: bottom tab bar (Home, Workouts, Timer, Log, More). Tap targets ≥ 44px.
- [x] Dark theme by default. Light theme available and persisted.
- [x] Unit system kg / lb persisted.
- [x] First launch seeds 3 sample templates so the home screen is not empty.
- [x] Works offline after first load (localStorage + optional service worker).

## 2. Exercise catalog

- [x] Built-in catalog grouped: Strength, Bodyweight, Core, Cardio.
- [x] Search by name.
- [x] Filter by category.
- [x] Add catalog item into a template, then set sets/reps/rest or work/rest/rounds.
- [x] Create a fully custom exercise name.

## 3. Create / edit / save workouts (templates)

- [x] Name the workout. Optional notes.
- [x] Add exercises from catalog or custom.
- [x] Each exercise is one of two kinds:

  **Sets** — sets, target reps, optional target weight, rest between sets (seconds).

  **Timer** — work seconds, rest seconds, rounds (work→rest cycles). No rest after the last round.

- [x] Reorder exercises (up / down).
- [x] Edit and delete an exercise.
- [x] Cannot save a workout with 0 exercises. Show a short reason.
- [x] Duplicate a workout.
- [x] Delete a workout with confirm.
- [x] Changes persist immediately after Save.

## 4. Log a live session (Hevy / Strong pattern)

- [x] Start from a template, or start an empty session and add exercises on the fly.
- [x] Each set row: previous performance | weight | reps | done checkbox.
- [x] Previous performance is the last saved session for that exercise name.
- [x] Checking Done starts the rest timer for that exercise (if rest > 0).
- [x] Skip rest. Pause / resume rest.
- [x] Add or remove sets during the session.
- [x] Finish session → duration + set count → written to History.
- [x] Option to save the finished session back as a new template.
- [x] Discard session with confirm (not saved).
- [x] Screen prefers to stay awake while a session is open (Wake Lock when the browser allows it).

## 5. Standalone timer (Tabata and friends)

- [x] Presets:
  - Tabata — 20s work / 10s rest / 8 rounds
  - Emom-style 60s × 10
  - 40/20 × 8
  - Custom work / rest / rounds / prepare
- [x] Big countdown. Clear WORK / REST / PREP label. “Round X of Y”.
- [x] Start, pause, resume, skip phase, reset.
- [x] Sound (Web Audio beep) + optional vibrate on phase change.
- [x] No rest after the final work interval → Done screen.
- [x] Optional: save the timed session to History with preset name + duration.
- [x] Screen stays awake while running when Wake Lock is available.

## 6. History & progress

- [x] History list: date, name, duration, exercise count.
- [x] Open a session to see every set (weight × reps or timed rounds).
- [x] Repeat last session (starts a new live log prefilled from that session).
- [x] Delete a session with confirm.
- [x] Home shows: last session, sessions this week, simple streak (consecutive calendar days with a session).
- [x] Personal record badge when a finished set is the heaviest weight for that exercise.

## 7. Settings & data

- [x] Theme: Dark / Light.
- [x] Units: kg / lb (display only; stored value is what the user typed).
- [x] Sound on / off. Vibrate on / off.
- [x] Export all data as JSON.
- [x] Import JSON (merges workouts + sessions).
- [x] Clear all data with typed confirm.

## 8. Out of scope for this MVP

- Accounts, cloud sync, multi-user
- Social / following / leaderboards
- Video form demos
- Wearables
- Charts beyond PRs + week count
- Subscriptions or IAP (web companion is free and local)

## 9. Success bar

- Build a 4-exercise Push day on desktop in under a minute.
- Run it on a phone: log a set in two taps, rest timer starts by itself.
- Run a Tabata without staring at the screen (beep on every switch).
- Close the tab, reopen, templates and history are still there.
