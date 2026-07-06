# BRIEF — asknewyork.ai landing page

Reproduce the **askaustralia.ai** landing page for **asknewyork.ai** — same architecture, structure,
behaviour and commercial purpose; **new aesthetic to be decided inside the new project**.
Structural reference: `~/Desktop/askaustralia/index.html` (single file — read it before building;
it is the freshest implementation of this template, "Red Centre" design language).

---

## 1. What this page is

- A **design-only, domain-for-sale landing page** for `asknewyork.ai`, fifth property in the
  Noustelos Studio "Ask" network (asksantorini.ai → asksingapore.ai → asksydney.ai →
  askaustralia.ai → asknewyork.ai).
- **One file: `index.html`.** Vanilla HTML/CSS/JS. No frameworks, no build step, no backend,
  no dependencies, no asset files (favicon and decorative art are inline SVG/data-URIs).
- The chat is a **SCRIPTED DEMO**: four hardcoded Q→A pairs matching the category chips play a
  typing-dots + word-by-word reveal; any other input gets a fallback line. Zero AI, zero network —
  a real backend may replace the scripted map later, so the wiring hooks (§7) must stay in place.
- **Commercial goal: sell the domain.** The `.acquire` pill above the topbar is the primary
  conversion point.

### Honesty rule (non-negotiable)
The demo must never fake live-AI signals:
- A bold `.caption` under the category chips discloses the scripted demo and links to the live
  concierge at **asksantorini.ai**. This is the only disclosure line — no separate `.disclaimer`.
- The chat-window status label reads **"Live Demo · Ask New York AI"** — "Live Demo", not "Live".
- The weather line is a static mockup (placeholder `id`, no fake "live" framing beyond the design).

---

## 2. Decided parameters (locked before this brief)

| Item | Decision |
|---|---|
| Acquisition contact | `mailto:info@asksantorini.ai?subject=Acquisition enquiry — asknewyork.ai` (plain mailto, **no forms**; switch to `info@asknewyork.ai` once that mailbox exists) |
| Sister links | Footer: **"Sister concierges · asksantorini.ai · asksingapore.ai · asksydney.ai · askaustralia.ai"** (all four). Demo-disclosure caption links to **asksantorini.ai** only (it is the live concierge). |
| Studio mark | Bottom-left, links to **noustelos.gr** |
| Chip categories | **Restaurants / Hotels / Broadway shows / Directions** — Car rental is swapped out (nobody rents a car in a subway city); "Broadway shows" is the authentically-NYC concierge ask. The other three stay localized. |
| Deploy | Repo: `https://github.com/noustelos/asknewyork` → **Cloudflare Pages, git-connected**, custom domain `asknewyork.ai`, push to `main` = instant live |
| Aesthetic | **Open — decided in the new project.** Keep the token *architecture* (§4), swap the values. |

---

## 3. Page anatomy (reproduce 1:1)

One `<section class="hero">` (min-height 100vh) with three layers:

**Layer 1 — ambient decoration** (`.deco-*`, `aria-hidden`, `pointer-events: none`):
- `.deco-uluru`-equivalent: ONE signature piece of thin line-art inline SVG anchored bottom-left
  (Australia uses Uluru with its runoff striations, a low sun faint behind, desert ripples and
  spinifex beneath — ~35 paths at stroke-opacity 0.08–0.45). New York motif candidates — decide
  with the aesthetic: the Midtown skyline with the Empire State and Chrysler spires, the Brooklyn
  Bridge gothic towers with their cable fans, the Statue of Liberty torch over harbour water,
  rooftop water towers over a brownstone cornice line. Static, no animation; recedes on
  mobile (`width: 80vw; opacity: ~0.45`).
- `.deco-weave`: full-bleed adaptive theme layer, transparent by default (`opacity: 0`,
  `transition: opacity .55s`). Query keywords dissolve a faint pattern in at **opacity 0.05**
  (Australia: spinifex dots for "outback", coral scallops for "reef", swell lines for "coast" —
  all as data-URI SVG / repeating-linear-gradient). New York themes TBD with aesthetic
  (e.g. art-deco sunburst or pinstripe for "luxury / Fifth Avenue", leaf scatter for
  "Central Park", cable/grid lines for "skyline / bridge", marquee dots for "Broadway / jazz").

**Layer 2 — `.inner`** (max-width 1340px, flex column), top to bottom:
1. `.acquire` pill — centered above the topbar. Uppercase tracked microcopy:
   *"Premium domain available for acquisition · Enquire →"* with a small diamond glyph.
   Quiet reserved-CTA-color **outline at rest, fills solid on hover**. This is one of only two
   places the reserved CTA color appears.
2. `.topbar` — left: brand (circular `.mark` containing a rotated-45° gradient `.diamond` +
   `ASKNEWYORK` wordmark in gradient text with the `.AI` tld in the accent color); right: the
   live-clock lockup (§5).
3. `.main` → `.hero-row` (flex, **non-wrapping** above 760px):
   - `.hero-left`: eyebrow *"New York · AI Concierge"* → giant display title **"Just / Ask"**
     (serif, `clamp(84px, 13.5vw, 176px)`, line-height 0.9, "Ask" in the accent color) →
     `.effortless` card (fit-content white panel: pip + "EFFORTLESS" label,
     *"No app. No sign-up. Just answers."*).
   - `.hero-right` (flex-basis ~414px): the chat mock (§6).
4. `.closing` — centered: italic serif guide line *"your New York AI travel guide."*, a lede
   (*"Restaurants, hotels, Broadway shows and live directions — instant local answers, without
   the noise."*), and an italic tagline (*"Your AI concierge, made for New York, in your pocket —
   ready any time, any day."*).
5. `.foot` — hairline + *"Sister concierges · [asksantorini.ai] · [asksingapore.ai] ·
   [asksydney.ai] · [askaustralia.ai]"* (uppercase tracked, links in accent color).

**Layer 3 — floating anchors** (absolute, z-index 3):
- `.cta-pill` bottom-right: white pill "Ask New York AI" with a ring+diamond icon; on click
  focuses the chat input (placeholder hook `#cta-ask`).
- `.studio-mark` bottom-left: "NOUSTELOS STUDIO" → noustelos.gr; on ≤760px it leaves the float and
  joins the flow under the footer (`margin: 6px auto 58px` to clear the CTA pill).

### `<head>` (the link preview IS the sales pitch)
- `<title>ASKNEWYORK.AI — Just Ask</title>`; meta description ending in
  *"Premium domain available for acquisition."*
- Canonical `https://asknewyork.ai/`, `theme-color` = page background, full OG + Twitter
  summary-card set (og:site_name, og:title, og:description mirroring the meta description).
- Inline SVG favicon as a data-URI: the diamond brand mark on the accent color (no asset file).
- JSON-LD `WebSite` block: *"New York AI concierge — premium domain available for acquisition."*
- Google Fonts `<link>` (preconnect ×2 + one stylesheet): one display serif + one UI grotesque —
  **families TBD with the aesthetic** (Singapore uses Newsreader + Hanken Grotesk; Sydney uses
  Fraunces + Albert Sans; Australia uses Young Serif + Figtree — pick a fourth pairing so the
  sisters stay distinct).

---

## 4. Styling system — keep the architecture, swap the values

All design decisions live as CSS custom properties in `:root`; **never hardcode colors at call
sites**. The token *shape* to reproduce (values are the new project's aesthetic decision):

- `--paper` (page field) and `--ink` (body text) — the neutral pair.
- One **accent family** (`--jade`/`--jade-deep` in Singapore, `--harbour`/`--harbour-deep` in
  Sydney, `--ochre`/`--ochre-deep` in Australia) — brand mark, links, live dots, focus rings,
  decorative art.
- One **reserved CTA color** (`--vermilion` in Singapore, `--sunset` in Sydney, `--eucalypt` in
  Australia) — used at EXACTLY two conversion points: the Send button and the acquisition pill.
  **Nowhere else.** This scarcity is the page's conversion logic — preserve it whatever the new
  palette is.
- `--mist` (soft surface/divider tint), derived alpha tints (`--ink-70/55/40`, `--ink-line`,
  `--accent-line`, `--accent-tint`), `--hero-bg` (paper base + two faint accent radial washes
  from opposite corners), gradients: `--diamond-grad`, `--wordmark-grad`, `--send-grad(+hover)`.
- `--font-display` / `--font-ui`.

### Motion & a11y rules (carry over verbatim)
- All keyframes prefixed and defined at the top of `<style>` (Singapore `sc*`, Sydney `sy*`,
  Australia `au*` — pick a new prefix, e.g. `ny*`): living-logo shimmer/pulse, Send glow + spark
  sweep, live-dot pulse, typing dots, and the staged `Rise` entrance
  (acquire → topbar → hero-left → hero-right → closing → foot → cta/studio, delays .08s–.66s).
- **No continuous full-surface animations, no `backdrop-filter`** — stays light on old machines.
- One `@media (prefers-reduced-motion: reduce)` block gates ALL motion; extend it for any new
  animation. Exception: the word-by-word streaming **still plays** under reduced motion
  (it's content presentation) — only dots, smooth-scroll and decorative animation drop.
- Global accent `:focus-visible` outline; the chat input row carries its ring via
  `:focus-within` (the field itself suppresses `outline`).
- Layout is **non-wrapping by design**; a single `@media (max-width: 760px)` fallback stacks the
  hero row, relaxes letter-spacing on tracked caps, wraps chips to 2×2, fades the deco art.

---

## 5. Live New York clock (topbar right)

Computed locally with `Intl.DateTimeFormat`, refreshed every 15s — no network.
**Single zone, single lockup** — `America/New_York` covers the whole city; collapse Australia's
dual-zone lockup back to Sydney's single-clock shape (`~/Desktop/asksydney/index.html` has it).
⚠️ New York observes DST (EST/EDT) — derive the label with `timeZoneName: 'short'` from the
formatter each tick (both sister implementations already do this — **never hardcode "EST"**).

Editorial lockup, top to bottom:
1. `.clock-date` — accent-colored tracked caps date line (e.g. "Mon, 06 Jul 2026").
2. `.clock-time` — large light-weight `HH<span class="cc">:</span>MM` numeral, tabular nums,
   dimmed watch-style colon. Decide with the copy pass: 24h like the sisters, or 12h with a small
   AM/PM cap — the US convention. Whichever, keep the dimmed-colon watch styling.
3. `.clock-meta` — pulsing live dot · **timezone label** (derived, see above) · availability
   tagline. Australia says "24/7 Coast-to-Coast Availability" — New York needs its own
   (e.g. "24/7 Five-Borough Availability" or "24/7 in the City That Never Sleeps"); decide with
   the copy pass.
4. `.clock-weather` — **static mockup** weather line with placeholder id (`#nyc-temp`),
   marked `TODO: wire to live data later`. ⚠️ Locale detail: the US reads **Fahrenheit** — decide
   with the copy pass whether the mockup shows `84°F · Sunny` (local voice) or stays °C for
   network consistency (a July build would be summer values either way).

---

## 6. Chat mock — structure & scripted behaviour

**Structure:** `.chat-frame` (1px gradient-border wrapper + soft double drop-shadow so the card
floats) → `.chat` (white, radius 27px) containing:
header (pulsing live dot + "LIVE DEMO · ASK NEW YORK AI" + two icon buttons: refresh ⟳ and a
diamond "more") → intro (`.chat-title` serif: *"AI New York Concierge. / Instant local answers,
without the noise."* + three pip bullets: *"Start with your neighborhood," / "your mood," /
"or what you need right now."*) → gradient hairline divider → `#chat-log` (nested scroll,
max-height 300px, thin accent scrollbar, `overscroll-behavior: contain`; greeting is the first
bot bubble — NOT "G'day": New York voice, e.g. *"Hey! I'm your local New York AI. Ask me
anything."*) → `.chips` row (4 buttons with `data-prefill`) → disclosure `.caption` →
`.input-row` (pill: input + reserved-CTA-family Send).

Bubbles: bot rows carry a small avatar (ring + diamond) and a mist bubble with radius
`4px 16px 16px 16px`; user rows right-aligned, one-step-deeper mist, mirrored radius, max-width 85%.

**Behaviour (inline `<script>`, IIFE, zero network):**
- `SCRIPTED` array of 4 `{q, a}` pairs + `FALLBACK` string. Matching: normalized
  (trim/collapse-whitespace/lowercase) exact equality with the prefill questions.
- `submitQuery()`: guard on empty/`busy` → spark the Send → append user bubble → clear input →
  `respond()`.
- `respond()`: `busy = true`; typing-dots bubble ~800ms → swap to empty bubble →
  `revealAnswer()` streams word-by-word at **45ms/word** (one `<span class="w">` per word,
  opacity-only fade; forced reflow before adding `.in`; keep scroll pinned to tail) →
  `busy = false`. Under reduced motion: skip dots and smooth scroll, stream at **30ms/word**
  with instant pop.
- Send button: `.is-ready` glow whenever input has text; `.spark` sweep replayed via
  remove-class → force reflow → add-class, cleared on `animationend`. Empty-input click:
  spark only. Enter mirrors Send.
- Chips: prefill input, focus it, refresh send state, apply theme, then **auto-send after
  300ms unless `busy`** (if busy, the prefill just waits in the field).
- Adaptive background: `THEMES` array of `{name, re}` keyword regexes → `detectTheme()` on every
  input event → `applyTheme()` swaps a `theme-*` class on `.hero` with a 280ms `weave-shift`
  fade-out/in dissolve. Keep the mechanism; New York keyword→theme maps TBD with aesthetic
  (e.g. broadway/show/jazz/theater, park/green/picnic, luxury/fifth avenue/soho/shopping,
  skyline/rooftop/bridge/brooklyn).
- Floating CTA click → `input.focus()`.

### Scripted content to write (New York copy pass, same voice as the sisters)
Four Q→A pairs, exactly matching the chip prefills. Answers: 60–90 words, warm concierge tone,
2–3 concrete *named* local options spanning price/mood range — **city-wide scope: spread the
four answers across different neighborhoods/boroughs so the page reads "all of New York",
not just Midtown** — always ending with a follow-up question. Suggested prefills (finalize in
the new project):
- Restaurants → "Where should I eat tonight in the West Village?"
- Hotels → "Find me a boutique hotel in SoHo."
- Broadway shows → "What Broadway show should I see this week?"
- Directions → "How do I get to the Statue of Liberty?"
`FALLBACK` mirrors the sisters': honest "this is a preview" + nudge to the chips + acquisition hint.
The input placeholder: "Where to eat tonight?" (or New York flavour).

---

## 7. Backend wiring hooks — keep these in place, exactly

`#ask-input` (chat input) · `#ask-send` (Send) · `#cta-ask` (floating CTA) ·
`.chip[data-prefill]` (chips) · `#nyc-temp` (weather placeholder) · `#chat-log`.
A future backend replaces only `SCRIPTED` + `respond()`; everything else stays.

---

## 8. Repo & deploy

1. New folder (suggested: `~/Desktop/asknewyork`): `index.html`, `CLAUDE.md`, `README.md`,
   `.gitignore`. Write CLAUDE.md in the same shape as askAustralia's (what-this-is, honesty rule,
   deploy warning, architecture, tokens, hooks). **Keep the README truthful** — it must describe
   the aesthetic actually shipped (askSingapore's README once drifted to a discarded design;
   don't repeat that).
2. GitHub repo `https://github.com/noustelos/asknewyork` → Cloudflare Pages, git-connected,
   custom domain `asknewyork.ai`.
   ⚠️ Push to `main` = **instant live**. Work on branches, merge deliberately.
   ⚠️ Add the git remote and push the initial commit **before** expecting anything on GitHub —
   the askAustralia build sat committed-but-local until the remote was added.
   After every push, **verify the deployment actually landed** (Pages dashboard) — the
   askSingapore webhook once died silently and needed a repo reconnect in the dashboard.
   Rollback = revert commit + push, or dashboard rollback.

## 9. Explicitly open (decide in the new project)

- Entire aesthetic: palette values, the two font families, the signature deco motif and the
  weave theme patterns/keywords, design-language name (Singapore's is "Garden City Precision",
  Sydney's is "Harbour Light", Australia's is "Red Centre").
- Final wording of the 4 Q→A pairs, fallback, greeting, availability tagline, weather mockup
  values (°F vs °C included).
- The clock format decision (§5): 24h like the sisters vs 12h AM/PM (US convention).
- Whether the wordmark tracking/size needs tuning ("ASKNEWYORK" is 10 characters — between
  ASKSYDNEY's 9 at 21px / 0.32em and ASKAUSTRALIA's 12 at 20px / 0.3em, so start between the
  two treatments and tune optically).
