# 🎾 Padel Night Tracker

A small web app for running a padel round-robin night from your phone.

Add your players, create custom rounds, assign players to teams, track who is
resting, run a countdown timer, record scores, and follow the leaderboard
throughout the session.

The app also supports **live sharing**, allowing other players to open a
read-only link on their phones and follow the current leaderboard in real time.

It was built with **Claude** through an iterative back-and-forth process:
describing the need, refining the design, testing the behavior, and fixing
issues round by round. It is a practical example of building a working product
through prompt engineering and AI-assisted development rather than
hand-writing every line.

## ✨ Features

### 👥 Fully Custom Setup

- Add your own players
- Edit and remove players
- Give the two teams custom names
- Create as many rounds as needed
- Assign players to Team A or Team B
- Leave players resting for a round
- Reassign players between teams

There are no hardcoded players, teams, or rounds.

### ⏱️ Configurable Round Timer

Set the duration of each round in minutes and seconds.

The default duration is **8 minutes**.

The timer includes:

- Start
- Pause
- Reset
- Automatic countdown
- Round completion handling

### 🔔 Audio Warnings

The app provides audio feedback during each round:

- A warning bell when **30 seconds remain**
- A finishing chime when the timer reaches **zero**

No audio files are required. The sounds are generated directly in the browser
using the **Web Audio API**.

Because of browser autoplay restrictions, the user needs to interact with
the page before audio can play.

### 🏆 Live Leaderboard

The Play tab includes a live leaderboard that automatically calculates player
totals from the recorded round scores.

Players are ranked according to their accumulated points across the rounds they
have played.

### 📡 Live Sharing

The app can generate a **read-only live link** from the Play tab.

This allows other players to follow the game from their own phones without
installing the app or logging in.

The shared view can follow:

- Player list
- Team names
- Rounds
- Scores
- Current round
- Leaderboard updates

Live synchronization uses **Supabase** as the backend relay.

The client uses the Supabase JavaScript library loaded from its CDN, while
the application stores the current shared session state in a Supabase
`live_sessions` table.

Live sharing is intended for casual padel sessions and should **not** be used
for private or sensitive information.

### 💾 Local Persistence

The application stores the local game state in the browser's
`localStorage`.

This means a page refresh does not normally remove:

- Players
- Team names
- Rounds
- Scores
- Current game state

Round history is also stored locally so previous sessions can be reviewed.

### 📱 Mobile Friendly

The interface is designed primarily for use on a phone during a padel session.

The layout adapts to smaller screens while keeping the timer, scores,
players, and controls easy to access.

## 🛠️ Tech Stack

The application is intentionally lightweight:

- **HTML5**
- **CSS3**
- **JavaScript**
- **Web Audio API**
- **Browser localStorage**
- **Supabase**
- **Supabase JavaScript Client**

The main application is contained in a single HTML file, with no frontend
framework and no build step.

Supabase is used only for the optional live-sharing functionality.

## 📁 Project Structure

```text
.
├── index.html       # Main application
├── vercel.json      # Static deployment configuration
└── README.md
```
