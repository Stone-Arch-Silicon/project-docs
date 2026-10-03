# Contributing, and adding a project to this site

One focused change at a time, with evidence attached. That is the whole contribution model.

## Contributing to an existing project

1. Pick the repository that **owns** the work and read its README.
2. Make one focused change with a stated problem and expected result.
3. Attach evidence: a rendered-page check for docs, or commands, logs, and reports for hardware.
4. Open a pull request so review and credit are recorded.

Do not assign authorship or review credit to anyone who has not agreed to it.

## Which repo owns what

| Change | Goes in |
| --- | --- |
| A course lesson | [ASIC 101](page_5.md) |
| Reference material not tied to a lesson | [ASIC Docs](page_8.md) |
| Docs styling or navigation | [ASIC Docs Theme](page_9.md) |
| Club-facing pages | [Club Website](page_14.md) |
| A project summary | this site |

Content in the wrong repo is the most common review comment. Check this table first.

## Adding a page here

```sh
cd Pages
cp TEMPLATE.md page_18.md    # next free number, no gaps
```

Rules the renderer enforces:

- Exactly one `# ` heading per file, on the first content line. It becomes the sidebar label.
- Numbering must be sequential. A gap stops page discovery at the gap.
- Raw HTML is escaped. Markdown only.
- Link pages by filename: `[stages](page_3.md)`.
- Commit images under `Pages/img/` and use relative paths.

## Keep project pages honest

- State the stage the artifacts support, per [the ladder](page_3.md).
- Name the next missing step, not the eventual ambition.
- Keep it short. A project page that needs scrolling belongs in that project's own docs.

## Checklist

- [ ] Change lives in the repo that owns it
- [ ] Evidence attached to the pull request
- [ ] Stage claim matches the artifacts
- [ ] Links verified on both GitHub and the rendered site
