# How the projects fit together

Eight repos, four tracks, and a small number of real dependencies. Most of the coupling is links; two are actual submodules.

## The dependency graph

```text
                        .github  (org profile)
                            │ links to everything
                            ▼
                     club website ◄──── ASIC_101 (CONFIG.mainSite)
                            │ Docs dropdown
              ┌─────────────┴──────────────┐
              ▼                            ▼
          ASIC_101                     ASIC-docs
              ▲                         │     │
              │ submodule src/quickstart│     │ submodule theme/
              └─────────────────────────┘     ▼
                            │          ASIC-Docs-Theme
                            │ links to
                            ▼
                       ASIC-tutor

   Mat_Mul_Systolic_Arrays        8-Bit_Posit
   (standalone, no dependencies)  (standalone, no dependencies)
```

## The only hard dependencies

| Consumer | Depends on | How |
| --- | --- | --- |
| ASIC Docs | ASIC Docs Theme | git submodule at `theme/`, pinned by SHA, **current** |
| ASIC Docs | ASIC 101 | git submodule at `src/quickstart/`, **pin is stale** |

Everything else is a hyperlink. Break a link and a reader gets lost; break a submodule and a build fails.

## Known breaks in the graph

- ASIC Docs' pin on ASIC 101 points at an August commit. Lessons changed since then do not appear in the book.
- That submodule's URL names the pre-rename `ASIC_101_quickstart` and survives only on GitHub's rename redirect.
- ASIC 101 contains **zero** references to ASIC Tutor, so the intended two-way link is one-way.
- The project directory is duplicated in three places with no sync. See [the drift problem](page_13.md).

## The two documentation stacks

```text
ASIC_101  ──  hand-written JS renderer, raw HTML escaped   ("the old renderer")
ASIC-docs ──  mdBook + shared theme, raw HTML allowed
```

Both are live and both render the same 25 lessons. No repo states which one wins. That is an open decision, not a settled architecture.

## Where the standalone projects attach

[Mat Mul](page_11.md) and [8-Bit Posit](page_12.md) have no code dependency on anything. They are where the course's skills get used on something new — and both would belong under ASIC Docs' "Additional Projects" chapter if anyone wrote them up there.
