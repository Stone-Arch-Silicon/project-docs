# Track: documentation

Two repos: one holds the writing, the other holds the look. The split exists so a styling change never touches prose and a prose change never touches CSS.

| Repo | Role | Stage |
| --- | --- | --- |
| [ASIC Docs](page_8.md) | The mdBook book: reference material and the course, mounted | Scaffold |
| [ASIC Docs Theme](page_9.md) | Shared mdBook theme and HDL syntax highlighting | Usable |

## How they connect

ASIC Docs mounts both the theme and the course as **git submodules**:

```text
ASIC-docs/
  theme/            → ASIC-Docs-Theme     (mdBook's default theme path)
  src/quickstart/   → ASIC_101            (the 25 lessons, rendered in-book)
```

So the book does not copy the course; it renders it. Clone recursively or the build produces an unstyled book with an empty tutorial chapter:

```sh
git clone --recurse-submodules <repo-url>
```

## Two renderers, on purpose

| | ASIC 101 site | ASIC Docs book |
| --- | --- | --- |
| Engine | Hand-written JS renderer | mdBook |
| Raw HTML | Escaped | Allowed, so `<iframe>` embeds work |
| Scope | The one guided project | Topic-organized reference |

The repos call the ASIC 101 renderer "the old renderer." Both are live; the book is the direction of travel.

## What belongs where

- A step in building the ALU → [ASIC 101](page_5.md).
- Reference material that generalizes past the ALU → ASIC Docs' RTL / Simulation / Place & Route sections.
- A small self-contained build that is not part of the course → ASIC Docs, "Additional Projects."
- Colors, fonts, navigation, code-block chrome → [the theme](page_9.md), never a consumer book.
