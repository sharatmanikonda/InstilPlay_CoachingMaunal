# InstilPlay Coaching Manual

Junior & youth cricket coaching (U8–U19): the syllabus, the coaching manual, and a mobile prototype of an 8-week Batting & Fielding program built on top of them.

## What's here

| File | What it is |
|---|---|
| `cricket-program.html` | Mobile app prototype (React 18 + htm, no build step). Coach and student views of the 8-week *Bat & Field Foundations* block, Day 1 in full detail, animated technique clips and drill diagrams, and student gamification (XP, levels, quests, badges, journey map, leaderboard). |
| `Cricket-Coaching-Syllabus.json` | The syllabus tree (parts → chapters → topics, drill categories) with stable ids. The app loads it at runtime and references topics by id. |
| `The-Coaching-Crease.html` | The full coaching manual, including the 102-drill library. |
| `Cricket-Coaching-Syllabus-MindMap.*` | The syllabus as a mind map (`.mm` for Freeplane/FreeMind, plus HTML and PDF exports). |
| `.claude/launch.json` | Local dev-server config used by Claude Code. |

## Run the app locally

The app fetches the JSON, so it must be served over HTTP (browsers block `fetch` from `file://`):

```bash
python -m http.server 5173
```

Then open <http://localhost:5173/cricket-program.html>. The layout is designed for phone width; on desktop it renders as a centred phone-sized column.

## Live site (GitHub Pages)

`.github/workflows/pages.yml` deploys on every push to `main`. It publishes **only** the app (as `index.html`) and `Cricket-Coaching-Syllabus.json`; the manual and mind-map files are not put on the site.

Site: <https://sharatmanikonda.github.io/InstilPlay_CoachingMaunal/>

One-time setup: **Settings → Pages → Build and deployment → Source: GitHub Actions**. A Pages site is public even when the repository is private.

## How the program maps to the syllabus

The 8-week plan lives in `cricket-program.html` (`PROGRAM`, `WEEKS`, `DAY1`) and never duplicates syllabus text: every topic is an id such as `ch9-t1` (Grip) or `ch12-t2` (Ground fielding), resolved to its title from the JSON. Drill numbers refer to the Drills Library in *The Coaching Crease*. Editing the JSON updates the app.

Student progress (XP, ticks, scores) is stored in the browser's `localStorage` only; it is a prototype, not a synced backend.
