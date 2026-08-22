# Station — Landing Page

Marketing site for **Station**, an AI assistant for academic time management. Station reads
your Canvas assignments and your Google / Apple calendars, then decides *when* the work
actually happens — and explains why.

## What's here

A single self-contained page: [`index.html`](index.html). No build step, no dependencies,
no framework. Open the file in a browser and it runs.

### Page structure

| Section | What it does |
| --- | --- |
| **Hero** | Centered type statement and the two calls to action. |
| **Live demo** | A working miniature of Station — see below. |
| **How it works** | Canvas-list vs. Station-day comparison, the three connectors, and a spec sheet. |
| **FAQ** | Eight accordions covering estimation, overrides, privacy, and other LMSes. |

### The live demo

The demo is real state, not a mockup. It runs on a seeded queue of four assignments
across four courses:

- **Start** runs the countdown, fills the progress ring, and flips to Pause. Hitting zero
  auto-logs the block.
- **Done** subtracts the session from the task's remaining hours. Work left re-queues at the
  back; finished work drops into the timeline struck through.
- **Skip** re-queues the task and stamps its block `moved`.
- **Replan** re-sorts by overdue, then by work remaining, re-times every block, and marks
  them all `moved`.
- Clearing the queue reveals an end state. **Reset demo** starts over.

## Design notes

Dark-first, with a full light counterpart. Three theme states are handled: an explicit
`data-theme` stamp in either direction, plus the unstamped default that follows
`prefers-color-scheme`. The toggle lives in the nav and persists to `localStorage`.

- **Type** — Familjen Grotesk (display), Instrument Sans (body), IBM Plex Mono (times,
  course codes, labels). Loaded from Google Fonts.
- **Color** — violet-biased neutrals, periwinkle accent. Course colors are a signal system
  rather than decoration: STAT pink, BIO green, ENGL periwinkle, PSY teal, with amber
  reserved exclusively for *now* and *overdue*.
- **Structure** — a fixed hour rail runs the full page height with an amber "now" hairline
  that tracks scroll position, so the page itself is shaped like a day.

Motion respects `prefers-reduced-motion`.

## Local preview

```sh
open index.html
# or, to serve it:
python3 -m http.server 8000
```

## Before this goes public

- [ ] The waitlist form shows a local confirmation and **discards the address**. Point it at
      a real endpoint (Formspree, ConvertKit, your own handler) before launch.
- [ ] The spec-sheet claims are placeholders — 10-day planning horizon, 25–50m sessions,
      free tier, iOS/Android in early access. Replace with what's actually true.
- [ ] FAQ answers about data handling and Canvas read-only access need to match your real
      privacy policy.
