# Club Website

The public front door: who we are, how to join, and where the projects live. One hand-written HTML file, no build step.

**Stage:** live at [stone-arch-silicon.github.io/stone-arch-silicon](https://stone-arch-silicon.github.io/stone-arch-silicon/). Structurally thin — the whole site is a single page.

## Sections

`#top` hero · `#about` · `#flow` (five stages) · `#ways` · `#calendar` · `#network` · `#sponsor` · `#join`

The nav's Docs dropdown has exactly two hardcoded links: ASIC 101 and ASIC Docs. **There are no project cards on the site itself** — the project directory lives only in `README.md`.

Interactive pieces: a three.js chip canvas, an animated background field, a hand-rolled Google Calendar month grid, and an animation kill switch.

## Layout

```text
index.html     the entire site — 1,779 lines, inline <style> and <script>
README.md      project directory, learning path, contributing rules, officers
assets/logo.png
.github/workflows/proof-html.yml    link and HTML validator
.github/workflows/auto-assign.yml   assigns new issues and PRs
```

Deployment is GitHub Pages' legacy branch build from `main` at `/` — there is no deploy workflow. `Proof HTML` runs on every push and gates broken links and malformed markup.

## Palette

The site uses its **own** dark palette, distinct from the docs theme: `--bg:#0f0e11`, `--maroon:#5e0a1d`, `--maroon-soft:#7a0019`, `--brass:#c2a068`, `--text:#e4dee2`. Fonts are Space Grotesk, Inter, and JetBrains Mono.

That divergence is a deliberate fork in branding, not a bug, but it means a color change has to be made twice.

## Start here

Edit `index.html` and push. Proof HTML validates it. For the directory, edit `README.md` — and remember [the drift problem](page_13.md).

## What is missing

- `pages/readme.md` contains the literal word `pages`; `assets/sm.md` is empty. The README lists `pages/` as "additional site pages" and none exist.
- `package.json` is an untouched scaffold — `"name": "demo-repo"`, `"description": "A sample package.json"` — with one dependency the site never uses.
- Open Graph tags are incomplete: `og:image` is still a relative path and there is no `og:url`. The in-file comment flags this.
- `umn_asic_club_logo_under_1mb_256colors.png` sits at the repo root unreferenced.
- A Google API key for the calendar is committed in `index.html`. The in-file comment says this is intentional and safe **given** referrer and API restrictions in Google Cloud Console. Confirm those restrictions are actually applied.
