# CLAUDE.md

Project context for Claude Code. Keep this file accurate as the project evolves.

## What this is

A **static academic project page** for the paper:

> **WebSP-Eval: Evaluating Web Agents on Website Security and Privacy Tasks**
> Guruprasad Viswanathan Ramesh, Asmit Nayak, Basieem Siddique, Kassem Fawaz
> WI-PI Lab, University of Wisconsin–Madison — **PETS 2026** (Privacy Enhancing Technologies Symposium)
> arXiv: https://arxiv.org/abs/2604.06367

The page is intended to be hosted on **GitHub Pages**. Content (abstract, methodology, results) is drawn from the paper PDF in this folder (`_USENIX_2026__Browser_Agent_Benchmark (2).pdf`).

## Files

```
index.html        # the whole page (one file)
styles.css        # all styling
assets/framework.png   # Figure 1 (the framework diagram, white background)
assets/extension-demo.gif         # animated demo: the Chrome extension setting initial state (Quora settings)
assets/extension-demo-poster.png  # first frame of the GIF, used as the click-to-play poster
README.md         # local preview + GitHub Pages deploy steps
*.pdf             # source paper (not deployed)
```

No build step, no framework, no dependencies. Plain HTML + CSS. Three tiny inline `<script>`s in `index.html`: the theme toggle, the BibTeX copy button, and the click-to-play GIF player. Google Fonts load from CDN (IBM Plex Mono, Inter, Newsreader).

## Preview locally

```bash
python3 -m http.server 8080   # then open http://localhost:8080
```

A server is often already running on 8080 during a session — just refresh.

## Page structure (sections, top to bottom)

`nav.topbar` → `header.hero#top` → `#abstract` → `#overview` → `#methodology` → `#results` → `#citation` → `footer`. Sections alternate background via `class="alt"` (currently: overview + citation are `.alt`). Each section opens with a `p.section-kicker` label, then an `h2`.

- **Hero**: `h1.title`, `p.tagline` (the long subtitle), `p.authors` (4 email links), `p.affil` (WI-PI Lab link + UW), `p.venue` (PETS pill), `.btn-row` (arXiv / Code &amp; Data), `figure.framework` (image + caption).
- **Overview**: motivating question, `ul.chips` (9 task categories), the state-control problem.
- **Methodology**: `.cards > .card` ×3 — Task Curation, Agent Instantiation, Automated Verification. Below the cards, a `.state-demo` subsection ("Setting Consistent Initial State") holds a click-to-play `figure.framework.state-figure` — a `button.gif-player` showing the poster PNG; clicking swaps `src` to `assets/extension-demo.gif` (the looping demo). Styled in `styles.css` under "Methodology: initial-state demo"; behavior in the bottom inline script.
- **Results**: `ul.findings` (RQ1–RQ4 + failure analysis) and a `table` (per-model success).
- **Citation**: terminal-style `.cite` block with BibTeX + copy button.

## Design system — "Cobalt Ledger" (with a red accent)

Disciplined security-tech look. Defined entirely with CSS custom properties in `:root` (light) and `html[data-theme="dark"]` (dark) at the top of `styles.css`.

- **One accent, used like a status indicator** — currently a pleasant **red** (`--accent` `#cc3b35` light / `#f2756b` dark). It appears on kickers, links, primary button, nav underline, card hover edge, findings left-rule, the venue pill, and (dark) the figure ring. Keep accent usage disciplined — do **not** reintroduce per-section rainbow hues.
- **Author links are blue** (`--author`) as a deliberate second color, distinct from the red accent.
- **Verified-green** (`--positive`) is reserved for the results table best row only.
- **Fonts**: IBM Plex Mono for "machine" labels (kickers, `RQ` tags, nav brand, table headers, BibTeX, step numbers); Inter for title/headings/body; Newsreader is the single serif moment (the tagline).
- **Hairlines over shadows**; squared geometry (8–12px radii); hover is the only place borders shift to accent.
- **Figure frame stays white in both themes** (`--figure-frame`) so the white-background PNG blends; dark mode adds an accent-tinted ring.
- **Theme**: toggled by the nav button; persisted in `localStorage`; an inline script in `<head>` sets it before paint (respects `prefers-color-scheme`).

To recolor the whole site, edit `--accent` / `--accent-dark` / `--accent-tint` in both `:root` and the dark block. Two earlier explored directions exist in the panel history (Editorial-Mono cardinal; Swiss Grid) if a different look is wanted.

## Editing notes / TODO hooks

- **Code &amp; Data button** links to `https://github.com/wi-pi/webspeval_code` (`id="github-link"`, opens in a new tab); labeled "Code &amp; Data" since the dataset lives in the same repo. It returned 404 when added on 2026-06-08 &mdash; expected if the repo is still private; it'll resolve once public.
- **The separate Dataset button was removed** (2026-06-09) &mdash; the data is in the code repo, so the hero `.btn-row` now has just two buttons: Paper (arXiv) and Code &amp; Data.
- **arXiv id** is `2604.06367` as provided by the author. (Note the format `YYMM.NNNNN` — `2604` = April 2026.)
- Section content mirrors the paper; if numbers change, update both the `.findings` list and the `table` in `#results`.

## User preferences observed

- Wants it **minimal and uncluttered**; dislikes redundancy (Contributions section was removed because it repeated the modules already in Abstract/Methodology).
- Disliked gradient/oversized titles — keep the title a clean solid color at a moderate size.
- Iterates visually via the local server; make focused changes and let them refresh.

## Changelog

Newest first. Append a dated entry when the page changes meaningfully.

- **2026-05-30** — Initial page built from the paper PDF: hero, abstract, overview (with task-category chips), methodology, results (findings + table), citation. Added light/dark theme toggle. Ran a design panel and adopted the "Cobalt Ledger" direction, then recolored the accent from cobalt to a pleasant red and set author links to blue. Removed a redundant Contributions section. Dataset and Code links are still placeholders (`href="#"`).
- **2026-06-08** — Added a "Setting Consistent Initial State" subsection under the three methodology cards: a click-to-play figure showing the custom Chrome extension replaying recorded actions to reset a website's state (Quora settings page). Presented as a static poster (`extension-demo-poster.png`, the GIF's first frame extracted via ffmpeg) with a red ▶ overlay; clicking swaps to the looping `extension-demo.gif`. Reuses the white-plate `figure.framework` look; has a graceful "coming soon" fallback if the asset is missing. New inline script handles the swap.
- _(add next entry here)_
