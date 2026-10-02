# ALAN·YU — personal site

<https://alan-yu-2077.github.io/>

The page opens with a 24-second film: the blue full stop of ALAN YU● comes to life and
walks through three pairs of keywords — Notion & Idea, Curiosity & Courage, Exploration &
Adaptability — and then the system around an LLM (tools, memory, guardrails, the loop).
It lands back in place: the film's last frame is the page's first screen. Then the page —
About, Stack, Experience, Projects, Education — where the same ball goes on as a guide: it
stands in each section's scene, jumps to the next one when the scroll stops, and acts out
whichever of About's four principles is pointed at.

- The site is React + Vite. The film is a Remotion composition that the page plays
  with `@remotion/player`; its night scene is three.js.
- Its score ("A6 · Cascade", D minor, half-time 120) is synthesised in Node — no
  samples — and mastered to −16 LUFS.
- The film plays on a first visit in a landscape window at least 1024 px wide with
  WebGL2. It is skipped under `prefers-reduced-motion`, Save-Data or the site's
  Motion switch, and on a repeat visit in the same session; phones play it on demand
  in a 16:9 dialog. Skip or Esc end it.
- Sound is on, but most browsers keep it silent until the first click.

| File | What it is |
| --- | --- |
| `index.html`, `assets/`, `audio/`, `landmarks/`, `brand/`, `apple-touch-icon.png`, `luna-hero.jpg` | The production build of the site (Vite output; hashed chunks). The source is not in this repository yet. |
| `resume.html` | One-page A4 résumé. Print to PDF straight from the browser; stacks to one column on phones. |
| `alan-yu-resume.pdf` | That page, printed. |
| `playground.html` | The previous site's playground: 11 realtime character-rendering scenes. Kept, no longer linked from the page. |
| `terminal.html` | The previous site as a shell — commands, themes, easter eggs. Kept, no longer linked. |
| `assets/favicon.svg`, `assets/apple-touch-icon.png`, `assets/luna-hero.jpg` | The previous site's icons and the Luna screenshot, still used by the pages above. |
| `INSPIRATION.md` | Reference index for the previous site: 23 ASCII / terminal-aesthetic resources, grouped by use. |
| `.nojekyll` | GitHub Pages serves the build as it is. |

Local preview: `python3 -m http.server 8377` → <http://127.0.0.1:8377/>

Deployed with GitHub Pages from `main`.

## The previous site (until 2026-09-30)

A static site, hand-written: no framework, no build step, no dependencies. Art
direction was ASCII, after [ertdfgcvb.xyz](https://ertdfgcvb.xyz/) (Andreas Gysin);
the page layout was after [brittanychiang.com](https://brittanychiang.com), rebuilt by
hand; the character-rendering layers were original. Its `index.html` is in the
history at commit `d6767ba`. The notes below describe that page, and the playground
and terminal, which are still here.

## The previous index.html — the two ASCII layers

One behind everything, one in place of the `<h1>`. Both run at 24 fps, cost
roughly 9% of a core together, and stop when the tab goes to the background.

### 1. Full-screen character field

8×11px cells tile the viewport (~11,700 of them at 1280×800) running a plasma
built from two diagonal waves interfering with one row wave. The pointer pushes
a ripple ahead of it; a click sends out an expanding ring.

It stays out of the way of the text through an **attenuation mask**: on every
layout or scroll change the bounding boxes of the body elements are rasterised
into a `Float32Array`, and wherever there are words the characters thin out and
drop to 20% brightness, with a 44px feathered edge. The field reads clearly in
the margins and all but vanishes under a paragraph.

The plasma is separable, so `sin(a+b)` is expanded into per-row and per-column
tables and each cell does a few lookups instead of four `sin()` calls — about
3× faster (21% → 10.6% of a core).

### 2. Tumbling voxel wordmark

`ALAN YU` is extruded from a 5×7 dot-matrix font into a voxel block
(`SUB=4`, `ZS=4` layers, 2.1 units thick) and rendered with a perspective
projection and a z-buffer into 4×6px character cells.

The camera and shading are the playground's `spin` scene — camera at `D=24`,
shading from depth alone over the ramp `' ·:;=+*#%@'` — but the motion is not.
`spin` turns continuously at 0.9 rad/s, which leaves the name legible only
within about ±20° of face-on: roughly one second in every seven, on the one
element that carries the site's name. Here the mark holds face-on for 5s, then
makes one full turn over 2s with smoothstep easing, and repeats; the first turn
comes at 3s so a visitor sees it early. The pitch and roll wobble and a ±7° yaw
sway keep running through the hold, so the slab still reads as a solid.

Two things that took measuring to get right:

- **Cell size, not glyph size.** An earlier pass ran 5×7 cells at font 9 and
  concluded that finer cells thin the strokes. They don't — as long as the font
  isn't scaled down with the cell. A stroke covering 1.6 cells at 5×7 covers 2.1
  at 4×6, and the letters read solid instead of skeletal: word 313→327px,
  columns across the word 81→101, mean ink unchanged. But the font must still
  *fit* the cell: at font 9 in a 4×6 cell every ramp glyph clips toward a filled
  block and the density ramp collapses, buying spatial detail with tonal detail.
  Font 7 keeps all ten steps distinguishable.
- **Perspective is nearly free; nodding is not.** Pulling the camera from D=90
  to D=55 cost 7% of the fitted width and bought 39% more near/far taper. A ±2°
  pitch wobble, by contrast, cost 13%. The two constraints run in different
  directions: the edge-on sweep of perspective is horizontal and the canvas is
  86 cells wide, while a nod is vertical and it is only 18 tall.

`spin` centres the word in its grid, which leaves the mark visibly indented from
the copy below it, so `fitTitle()` re-derives the face-on pose from the same
formula and pulls the canvas left by exactly that inset.

### Accessibility and fallbacks

- The `<h1>` carries the real text "Alan Yu", visually hidden, and the canvas is
  `aria-hidden`. Screen readers, search engines and text-only modes all get the
  name itself.
- **Pause button** (bottom of the left column). Motion that autoplays, runs
  longer than five seconds and sits alongside content needs a user-operable
  pause under WCAG 2.2.2 — `prefers-reduced-motion` does not satisfy it. The
  choice is remembered in `localStorage`.
- The clock accumulates rather than reading absolute time, so pausing holds the
  current pose and resuming does not jump. Click ripples are stamped with the
  same clock; stamping them with `performance.now()` made them lag by every
  second the page had spent paused or in a background tab.

| | Effect |
| --- | --- |
| Pause button | Both layers stop redrawing (the field still answers the pointer); a wordmark caught mid-turn snaps to the end of that turn. The choice is remembered |
| `index.html?bg=off` | Both layers removed; the heading falls back to plain bold text |
| `index.html?bg=static` | Frozen at `t=0`; the character field still follows the pointer |

Automatic degradation: `prefers-reduced-motion` freezes both layers; touch
devices freeze only the character field (it is pointer-driven, so there is
nothing to show without one) while **the wordmark keeps turning** — the rotation
is the design, and phone users should still see it. A frozen field is still
redrawn on scroll (once per frame), so its attenuation mask keeps following the
text.

## playground.html — playground

`ALAN·YU` in the header goes back to the site. `playground.html#s=N` opens scene
N (1-based) and follows the hash when it changes.

| Key / action | |
| --- | --- |
| `1`–`9` `0`, or click the menu | Scene (plasma / donut / metaballs / waves / flow / type / alan·3d / spin / orbit / morph / flag) |
| `←` `→` | Previous / next scene |
| `space` | Pause |
| `i` | Invert (dark ground ↔ paper white) |
| Move the pointer | Ripples in plasma / waves; head-tracking in alan·3d |
| Click | Drop a ripple |

The whole viewport is a grid of equal-width character cells. Every frame, each
cell computes a brightness from `(x, y, t, pointer)` and maps it onto a density
ramp such as ` .:-=+*#%@`, so tone is carried entirely by how much ink a glyph
has. Rendering goes through a glyph atlas — each character pre-rendered at four
alpha tiers, then blitted per cell with `drawImage`, which is far faster than
`fillText` per cell and holds 60fps full-screen.

Four of the scenes (`spin`, `orbit`, `morph`, `flag`) share one voxel point
cloud and differ only in their per-frame transform.

## terminal.html — the site as a shell

Boot self-test and a dot-matrix banner, then a prompt.

| Command | |
| --- | --- |
| `help` | Command list (there are hidden ones; `ls` is a start) |
| `about` / `projects` / `contact` | Content |
| `theme [dark\|green\|charm\|paper]` | Four themes, persisted to `localStorage` |
| `crt` | CRT scanlines and glow |
| `figlet <text>` | 5×7 dot-matrix banner text (A–Z, 0–9) |
| `play [1-11]` | Jump to a playground scene (`playground.html#s=N`) |
| `donut` / `matrix` | Full-screen easter eggs (`esc` or click to exit) |

Tab completion for commands and arguments, `↑` `↓` history, `Ctrl+L` to clear,
click anywhere to focus, block cursor.

## Tunables

Character field — `CW`/`CH` (cell), `TIERS` (brightness steps), `FPS`.
Wordmark — `T_CW`/`T_CH`/`T_FONT` (cell and glyph size), `T_D`/`T_Z0` (camera
distance and depth offset), `SUB`/`ZS`/`DEPTH` (voxel density and slab
thickness), `ADV` / `SPACE_ADV` (letter and word spacing), `HOLD`/`SPIN`/
`FIRST_SPIN` (the turn schedule, in `yawAt`), and the pitch/roll rates in
`drawTitle`.
Playground — `RAMP10` and friends, `FS`/`LH`, `MARQUEE` + `GLYPHS`, `--bg`/`--fg`.
Terminal — `FS` (fake filesystem), `CMDS` (command registry), `THEMES`, `GLYPHS`.

## Still to do

- [ ] Writing section — engineering notes drawn from Luna's per-version log
- [ ] LinkedIn link (the placeholder LinkedIn and Instagram icons were removed)
- [ ] Project thumbnails beyond the one Luna screenshot — agent-kernel's trace viewer first
- [ ] Self-host the fonts (Archivo, IBM Plex Mono), the one request the site makes to another host
- [ ] Put the site's source in this repository
- [x] Deploy — GitHub Pages, from `main` (the redesign since 2026-09-30)

## License

Code is MIT (see `LICENSE`). The build bundles third-party libraries under their own
licenses (React and three.js: MIT; Remotion: the Remotion License). The Eiffel Tower in
`landmarks/` is "SM - Eiffel Tower" by Scott Marshall (CC BY 3.0, via Poly Pizza),
preprocessed; the page credits it under Education. The résumé text, the Luna screenshot,
the preview card, the film and its score are © Alan Yu.
