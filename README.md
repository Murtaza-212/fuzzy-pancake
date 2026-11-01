# ATHLETIC TRANSFORMATION PROTOCOL — 365 DAYS. ONE TRANSFORMATION.

A 365-day home training app with a real progression engine, built in the visual style of `baki-protocol.html`.
Plain HTML, CSS and JavaScript. **No build step, no dependencies, works offline** (only the Google Fonts are fetched).
Your data stays in your browser (`localStorage`). Dark and light mode included (toggle top right).

## Put it on GitHub Pages (about 2 minutes)

1. Create a new repository on GitHub (for example `atp`), public or private with Pages enabled.
2. Upload **the contents of this folder** (not the folder itself) so `index.html` sits at the repo root.
   Web UI: *Add file → Upload files*, drag everything in, *Commit*.
   Or from a terminal:
   ```bash
   git init && git add . && git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
3. Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save.**
4. After a minute your app is live at `https://<you>.github.io/<repo>/`.

You can also just double-click `index.html` to use it locally.

## First run

- Open **SYSTEM**. Day 1 defaults to the next Monday. Day 1 is a Monday-style *Upper Body A* session and the weekly pattern follows programme days, so start on a Monday if you can.
- Check your Day 1 benchmarks (pre-filled from your profile). The Day 365 report compares against them.
- **Export a backup regularly** (SYSTEM → Export backup). Browser data can be cleared; GitHub Pages cannot save it for you.

## What is inside

| Area | What it does |
|---|---|
| **Train** | Today's session (Day N / 365, week, block, warm-up, exercises, rest, dumbbell options). Every set is its own tick with its own weight and reps/seconds field. An exercise is only "Completed" when every set is ticked. |
| **Programme** | The 13-block timeline with completion, what each block can unlock, and a 28-day calendar per block. Jump to any day. |
| **Progression** | Recommendations that wait for your approval, every pathway (current, previous, next, requirements, achieved, approval status), dumbbell load table, decision history. |
| **Training Log** | Full session history with per-set records, CSV export, and Day 1 vs 30 / 30 vs 60 / 60 vs 100 / 100 vs 180 / 180 vs 270 / 270 vs 365 comparisons plus custom days. |
| **Library** | ~90 exercises with muscles, equipment, steps, cues, common mistakes and easier options. Click any exercise name anywhere. |
| **Safety** | Flagged exercises, modification requests, gated movements. |
| **System** | Name, start date, theme, benchmarks, backup, import, reset (type `RESET`). |

## How the programme is built

- Exactly 365 days: 52 weeks (13 blocks × 4 weeks) + **Day 365 = annual assessment**.
- Fixed weekly template: Mon Upper A · Tue Cardio & Mobility · Wed Lower & Core A · Thu Yoga & Recovery · Fri Full Body B · Sat Conditioning · Sun Rest.
- Block 1–13 content follows your spec. Every 4th week is a **deload** (about half the working sets, no new variations, finish sets with 3+ reps in reserve).
- Block 3 is a technique block: it prescribes paused floor presses, tempo goblet squats and tempo Romanian deadlifts for those four weeks.
  After that, each slot returns to **your earned level** in its pathway.
- Block 13 week 2 is a reassessment week (work sets to a technical limit, no 1-rep maxes); Day 365 has a benchmark form.
- No jumping, sprinting, burpees, clap push-ups or other impact work, and no pull-ups (no bar assumed).

## The progression engine

- **Double progression** for dumbbell lifts: hit the top of the rep range on *every set*, tick *"clean technique, about 2 reps in reserve"*, in **two consecutive sessions** (deload weeks neither count nor break the run). Then the engine recommends, in this order:
  1. the next weight (10 → 20 → 30 lb) *if the jump is reasonable* (≤ 100 % for large lifts, ≤ 50 % for small lifts like curls and lateral raises);
  2. otherwise a **rep-range extension**, then a **3-second lowering tempo**;
  3. only then the big jump, or the next exercise level.
- **Bodyweight and timed exercises** use the same rule, then recommend the next pathway level (e.g. standard → slow-tempo → diamond *or* decline → archer → assisted one-arm), only from the block in which that level unlocks. Until then the target is extended instead.
- **Nothing changes without your approval.** You can *Stay at this level* (two more qualifying sessions before you are asked again) or *Step back a level* at any time. History is never deleted.
- **Flag discomfort** on any exercise: it is marked for review, progression pauses, history stays, and you can request a modification. No diagnosis is made.
- Loaded single-leg work (split squats, Bulgarian split squats, single-leg bridge, calf raise and RDL) is **gated**: it needs an explicit readiness confirmation and is never an automatic milestone, given your reported knee and ankle discomfort. Consider a professional assessment if discomfort recurs.

## Things to know (honest limitations)

- Ticking a set pre-fills the target top value; **edit it if you did fewer or more**, because the engine trusts what is recorded.
- Circuit stations (Block 10 Fridays) and reassessment sets are logged but do not drive progression.
- Cycling follows the programme's schedule; it is recorded (minutes, resistance, effort, distance) but is not auto-progressed.
- Day 1 starting weights are only *suggestions* (e.g. 20 lb floor press, 10 lb shoulder press). Choose what lets you hit the target with 2 reps in reserve.
- The Day 365 "weaknesses" and "next phase" are simple rules over your recorded data, not coaching or medical advice.
- Data is per browser and per device. Use Export/Import to move it.

## Extending it

Add an exercise in `js/ex-*.js` with `ATP.library.add(id, name, {...})`, then optionally slot it into a pathway in `js/pathways.js`
(each level has an unlock block `ub`, and `gated: true` for readiness-gated moves). Session content lives in `js/programme-plan.js`.

## Tests

```bash
npm install          # only needed for the UI test (jsdom)
npm test             # engine and programme tests (no dependencies)
npm run test:ui      # jsdom smoke test of the interface
```
