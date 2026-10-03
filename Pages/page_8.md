# ASIC Docs

The club's mdBook documentation book. Writers touch only markdown; mdBook and GitHub Actions do the rest.

**Stage:** scaffold. One substantive original page, four empty section stubs, and the course mounted from elsewhere. The README still reads "Fork this repo to start a new docs book."

Live at [stone-arch-silicon.github.io/ASIC-docs](https://stone-arch-silicon.github.io/ASIC-docs/).

## Outline

| Chapter | State |
| --- | --- |
| Introduction | Written — three pillars, prerequisites |
| 1. Quick Start Tutorial | 25 pages, mounted from [ASIC 101](page_5.md) |
| 2. RTL | Stub |
| 3. Simulation | Stub |
| 4. Place & Route | Stub |
| 5. Additional Projects | One page: 5-stage SKY130 ring oscillator |
| 6. Appendix | Stub |

Each stub says the Quick Start Tutorial already covers the topic as part of building the ALU. The sections exist to hold reference material that generalizes beyond the one project.

## Layout

```text
book.toml          mdBook manifest; wires theme/theme.css and theme/theme.js
src/SUMMARY.md     the chapter manifest — a page is invisible until listed here
src/introduction.md
src/TEMPLATE.md    copy-to-start page template
src/ringOscillator.md    ring oscillator + the formatting reference
src/quickstart/    submodule → ASIC_101
theme/             submodule → ASIC-Docs-Theme
.github/workflows/deploy.yml
```

## Start here

```sh
git clone --recurse-submodules <repo-url>
mdbook serve        # http://localhost:3000, rebuilds on save
```

To add a page: copy `src/TEMPLATE.md`, list it in `src/SUMMARY.md`, push to `main`. CI pins mdBook 0.4.36, builds, and deploys to Pages.

## What is missing

- **RTL, Simulation, Place & Route, and Appendix are unwritten** — each is a "still being written" placeholder.
- `book.toml` still carries the unreplaced placeholder `site-url = "/EDIT-ME-repo-name/"`.
- The `src/quickstart` submodule pin is **stale** — it points at an August commit of ASIC 101, so lessons changed since then do not appear in the book.
- That submodule's URL still names the pre-rename `ASIC_101_quickstart` and works only through GitHub's rename redirect. Fragile; worth updating.
- `src/ringOscillator.md` links to `page_2.md`, which does not resolve from `src/`. With `create-missing = false`, that is a dead link.
- Ring oscillator checklist is unfinished: ss/ff corners not swept, layout not drawn, DRC and LVS not run.
- `src/introduction.md` needs a copy-edit — several typos and one sentence comparing an ASIC to "an ASIC chip."
