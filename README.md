# asknewyork.ai

Design-only landing page for **asknewyork.ai** — fifth property in the Noustelos Studio "Ask" network
([asksantorini.ai](https://asksantorini.ai) → [asksingapore.ai](https://asksingapore.ai) →
[asksydney.ai](https://asksydney.ai) → [askaustralia.ai](https://askaustralia.ai) → asknewyork.ai).

Everything is a single file, [index.html](index.html): vanilla HTML/CSS/JS, no frameworks, no build
step, no backend, no asset files (favicon and decorative art are inline SVG).

## What it does

- **Sells the domain.** The acquisition pill above the topbar is the primary conversion point
  (plain `mailto:`, no forms).
- **Previews the concierge concept.** The chat window is an honest **scripted demo** — four
  hardcoded Q→A pairs behind the category chips (Restaurants / Hotels / Broadway shows / Directions),
  with a typing-dots + word-by-word reveal. The four answers deliberately spread across the city
  (the West Village, SoHo and Williamsburg, Broadway, the harbor and the Staten Island Ferry).
  Zero AI, zero network; a disclosure caption links to the live concierge at asksantorini.ai.
- **Live New York clock** in the topbar via `Intl.DateTimeFormat` — a single `America/New_York`
  lockup in the US 12-hour convention with a small AM/PM cap, the EST/EDT label derived from the
  formatter (New York observes DST). The weather line is a static Fahrenheit mockup awaiting
  live data.

## Design — "Gotham Deco"

Brass-and-ivory Manhattan art deco: ivory-marble paper (`#F7F3EA`), charcoal ink (`#1C1B18`),
Gotham brass (`#8C6A2F`) as the accent family — like lobby metalwork — and deep deco emerald
(`#14453D`) strictly reserved for the two conversion points (Send button + acquisition pill).
Signature decoration: thin line-art of the Midtown skyline — the Empire State's stepped setbacks
and spire beside the Chrysler's terraced crown, a full moon faint behind, a rooftop water tower
on the low block. Type: **Playfair Display** (display serif) + **Jost** (UI). All tokens live in
`:root` — see [CLAUDE.md](CLAUDE.md) for the full architecture.

## Run

No build. Open `index.html` in a browser, or:

```bash
python3 -m http.server 8000   # http://localhost:8000
```

## Deploy

Cloudflare Pages, git-connected: **push to `main` = instant live** on asknewyork.ai.
Work on branches, merge deliberately, and verify the deployment landed in the Pages dashboard
after every push.
