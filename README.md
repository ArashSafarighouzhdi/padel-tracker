# Padel Night Tracker

A small web app for running a padel round-robin night from your phone: add
your players, build your own rounds (who plays who, who's resting), run a
countdown timer per round with a warning bell before time's up, log scores,
and watch a live leaderboard update as you go.

It was built with **Claude**, through an iterative back-and-forth: describing
the need, refining the design, and fixing behavior round by round — a
practical example of building a working product through prompt engineering
and AI-assisted development rather than hand-writing every line.

## What it does

- **Fully custom setup** — no hardcoded players, teams, or rounds. You add
  your own players, name your two teams, and build as many rounds as you
  want by tapping players to assign them to a team or leave them resting.
- **Configurable round timer** — set the length in minutes and seconds
  (defaults to 8:00), with Start / Pause / Reset controls.
- **30-second warning bell** — an audio cue fires when 30 seconds are left
  in a round, plus a finishing chime at zero. No sound files — it's
  generated in the browser with the Web Audio API.
- **Live sharing** — generate a read-only link from the Play tab so anyone
  (no login, no app) can watch the leaderboard and current round update in
  real time on their own phone. Sharing uses a free, no-signup key-value
  relay ([kvdb.io](https://kvdb.io)) as a simple sync layer — good enough
  for a casual night with friends, not meant for private or sensitive data.
- **Live leaderboard** — recalculates automatically from saved round scores,
  ranking players by total points across the rounds they've played.
- **Works offline / no backend** — everything runs client-side, and progress
  is saved to the browser's `localStorage`, so a refresh won't lose your
  data.

## Tech

Plain HTML, CSS, and JavaScript in a single file — no framework, no build
step, no dependencies. Chosen deliberately so it can be deployed anywhere
(Vercel, Netlify, GitHub Pages, or just opening the file) with zero setup.

## Run locally

Just open `index.html` in a browser, or serve it:

```bash
npx serve .
```

## Deploy to Vercel

### Option A — Vercel CLI
```bash
npm i -g vercel
vercel --prod
```

### Option B — GitHub + Vercel dashboard
1. Push this folder to a GitHub repo.
2. Go to https://vercel.com/new and import the repo.
3. Framework preset: **Other** (it's a static site — no build command needed).
4. Deploy.

## Project structure

```
.
├── index.html      # the entire app: markup, styles, and logic
├── vercel.json      # static deployment config (clean URLs)
└── README.md
```

## Notes

- The 30-second warning bell needs one user interaction (tapping Start)
  before it can play — a browser autoplay restriction, not a bug.
- "Reset everything" requires tapping twice (arms, then confirms) instead of
  a native `confirm()` dialog, since some in-app browsers block those.
