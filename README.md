# Stone Arch Silicon: project directory

What every Stone Arch Silicon project is, what stage it is actually at, and where its code lives. One page per project, organized by track, rendered straight from markdown.

**Status:** current as of 2026-10-03. Stage claims are drawn from each repository's own artifacts, not from intentions.

## Start here

1. [What Stone Arch Silicon is building](Pages/page_1.md) — the eight repos, in one table.
2. [How the projects fit together](Pages/page_2.md) — the dependency graph and its known breaks.
3. [Project stages](Pages/page_3.md) — what each stage claim requires as evidence.

## Site map

| Track | Pages |
| --- | --- |
| Framing | [1: Overview](Pages/page_1.md), [2: How they fit together](Pages/page_2.md), [3: Stages](Pages/page_3.md) |
| Curriculum | [4: Track](Pages/page_4.md), [5: ASIC 101](Pages/page_5.md), [6: ASIC Tutor](Pages/page_6.md) |
| Documentation | [7: Track](Pages/page_7.md), [8: ASIC Docs](Pages/page_8.md), [9: ASIC Docs Theme](Pages/page_9.md) |
| Hardware and research | [10: Track](Pages/page_10.md), [11: Systolic Matrix Multiplier](Pages/page_11.md), [12: 8-Bit Posit](Pages/page_12.md) |
| Infrastructure | [13: Track](Pages/page_13.md), [14: Club Website](Pages/page_14.md), [15: Org Profile](Pages/page_15.md) |
| Shared | [16: Toolchain and site pattern](Pages/page_16.md), [17: Contributing](Pages/page_17.md) |

Every project page answers the same five questions: what it is, what stage it is at, what is in the repo, where to start, and what is missing.

## Project stages at a glance

| Project | Stage |
| --- | --- |
| ASIC 101 | Course material in development |
| ASIC Tutor | In development, private |
| ASIC Docs | Scaffold |
| ASIC Docs Theme | Usable |
| Systolic Matrix Multiplier | Synthesis — blocked on pin count |
| 8-Bit Posit | Concept — specification only |
| Club Website | Live |
| Org Profile | Live |

Stage definitions and the evidence each requires are in [page 3](Pages/page_3.md).

## Repository guide

| Path | Purpose |
| --- | --- |
| [Pages/](Pages/) | Project pages and images |
| [Pages/TEMPLATE.md](Pages/TEMPLATE.md) | Starting point for a new page |
| [app.js](app.js) | Site configuration, navigation, and the markdown renderer |
| [index.html](index.html), [style.css](style.css) | Static site shell |

To preview the site, serve the repository root over HTTP:

```sh
python3 -m http.server 8000
```

Open http://localhost:8000. There is no build step and no package installation.

## Contributing

Add a page by copying `Pages/TEMPLATE.md` to the next free `page_N.md`. The rules the renderer enforces:

- Exactly one `# ` heading per file, on the first content line. It becomes the sidebar label.
- Numbering must be contiguous. **The first missing number stops page discovery**, hiding every page after it.
- Raw HTML is escaped. Markdown only.
- Link pages by filename: `[stages](page_3.md)`.
- Commit images under `Pages/img/` and reference them by relative path.

Keep project pages short and state the stage the artifacts support, not the eventual ambition. Full guidance is on [page 17](Pages/page_17.md).

## Related Stone Arch Silicon work

- [Club website and project directory](https://github.com/Stone-Arch-Silicon/stone-arch-silicon)
- [ASIC 101 course](https://github.com/Stone-Arch-Silicon/ASIC_101)
- [ASIC documentation book](https://github.com/Stone-Arch-Silicon/ASIC-docs)
- [Shared mdBook theme](https://github.com/Stone-Arch-Silicon/ASIC-Docs-Theme)
- [Systolic matrix multiplier](https://github.com/Stone-Arch-Silicon/Mat_Mul_Systolic_Arrays)
- [8-bit posit research](https://github.com/Stone-Arch-Silicon/8-Bit_Posit)
