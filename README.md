# Trip Planner

A single-file trip board that runs in the browser. No build step, no backend required:
open `index.html` and it works.

**Live demo:** https://dereckcb.github.io/trip-planner/ - the trips are made up, and everything
you change stays in your own browser.

![board](docs/screenshot.png)

## What it does

- **Ideas backlog** for trips you want to take one day, no dates needed, then a kanban as they
  become real: **Planning, Booked, Ready, Ongoing, Done**. Drag a card across.
- **Every trip is one card**: dates with a live countdown ("in 24d", "ongoing", "12d ago"), who
  is coming, transport, where you sleep, budget against what you have spent, places and ideas,
  links, notes, and a **To do / Done** checklist you tick as you book things.
- The card shows what matters at a glance: countdown, dates and length, checklist progress, and
  what is left of the budget (red once you are over).
- Archive the trips you decide not to take instead of deleting them.
- **Light and dark**, and it works on a phone.

## Your data

Everything lives in `localStorage` under `trips_state`. Settings gives you a JSON **Backup** and
**Restore**, and the app keeps a rolling ring of the last 15 states as a safety net.

Optional: add Supabase keys at the top of the script and the app switches on accounts and
cross-device sync, with versioned history. Without keys it stays in demo mode - no login, no
network. See `SETUP.md`.

## Part of a set

Three small apps that share a look and a menu but nothing else - separate data, separate repos:

| App | Repo |
|---|---|
| Task Tracker | https://github.com/DereckCB/task-tracker |
| Job Search | https://github.com/DereckCB/job-search |
| Trip Planner | this one |

## License

MIT (c) 2026 Dereck Barinotto
