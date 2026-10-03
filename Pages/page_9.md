# ASIC Docs Theme

The shared mdBook visual layer: maroon and gold, dark, twin-arch motif, plus Verilog/SystemVerilog/VHDL syntax highlighting. Mounted as a submodule by any book that wants the club look.

**Stage:** usable and stable for its scope. Small, finished, no open TODOs — but no tags, no CI.

## What it overrides

It is **not a fork of mdBook**. It layers on sanctioned override points only, which is what keeps it upgrade-safe.

| File | Does |
| --- | --- |
| `theme.css` | The whole reskin. One `:root` block drives the palette and remaps mdBook's own CSS variables, so stock elements inherit without per-selector overrides. |
| `theme.js` | Scroll progress bar, right-hand scroll-spied "On this page," code-block caption bars, prev/next pager, footer. |
| `head.hbs` | Google Fonts: JetBrains Mono, Karla, Zilla Slab. |
| `header.hbs` | Brand bar above mdBook's menu bar, with the logo inlined as base64. |
| `highlight.js` | Custom highlight.js 10.1.1 build: mdBook's languages plus VHDL and a patched Verilog grammar. |
| `highlight-src/verilog.js` | The patch source of record. |
| `favicon.svg` | Chip-and-arch tab mark. |

`index.hbs` is deliberately untouched.

## The HDL patch

One grammar covers Verilog and SystemVerilog (`v`, `sv`, `svh`, `systemverilog`). Two changes over upstream:

1. The declared name after `module`, `interface`, `package`, `class`, `covergroup`, and friends is titled. `task` and `function` are excluded on purpose — an optional return type sits between the keyword and the name, and a regex cannot tell them apart.
2. Attribute instances `(* ... *)` are colored as metadata, matching the existing backtick-directive handling.

## Using it

```sh
git submodule add <theme-repo-url> theme
```

`theme/` is mdBook's default theme path, so no `book.toml` theme override is needed. Add:

```toml
additional-css = ["theme/theme.css"]
additional-js  = ["theme/theme.js"]
```

Those paths resolve from the **book root**, not the theme directory. To bump: `git checkout <ref>` inside `theme/`, then commit the new pointer.

## Re-theming

Edit `theme.css`'s `:root` block alone. Nothing in the theme names a specific club — the wordmark and repo link come from the mounting book's `book.toml`. The logo PNG is the only org-specific artifact.

## What is missing

- **No tags or releases**, so consumers pin raw commit SHAs.
- **No CI**, so a broken theme is only discovered by a consumer's failing build.
- The theme documents itself against **mdBook 0.5**, but its only consumer ([ASIC Docs](page_8.md)) pins **0.4.36**. Worth reconciling; the README's rebuild procedure covers a version bump.
- The logo must be re-embedded by hand (trim, resize, base64) to change it.
- Rebuild `highlight.js` from `highlight-src/`, never from a fresh `npm pack`, or the Verilog patch is silently lost.
