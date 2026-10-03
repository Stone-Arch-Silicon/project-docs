# Track: infrastructure

The two repos that route people. Neither contains hardware; both exist so a visitor finds the right project in one click.

| Repo | Role | Stage |
| --- | --- | --- |
| [Club Website](page_14.md) | Public site, recruiting, project directory | Live |
| [Org Profile](page_15.md) | The landing README on github.com/Stone-Arch-Silicon | Live |

## The routing graph

```text
github.com/Stone-Arch-Silicon  →  .github/profile/README.md
                                        ↓
                            club website (stone-arch-silicon)
                                        ↓
                      ASIC 101  ·  ASIC Docs  ·  project repos
                                        ↑
                     ASIC 101's CONFIG.mainSite points back here
```

## The drift problem

The project directory exists in **three** places — the org profile README, the club website README, and this site — with no automation keeping them in sync. They were last written together on the same day, which is the only reason they currently agree.

When a project's stage changes, update all three or pick one as canonical. The contact email already shows the symptom: the club README says `umnasicclub@gmail.com`, the ASIC 101 site says `umnasicgroup@gmail.com`, and a commit message mentions `SASI@umn.edu`.

## Two site stacks, not one

| Stack | Used by |
| --- | --- |
| `app.js` markdown renderer, no build | [ASIC 101](page_5.md), this site |
| mdBook | [ASIC Docs](page_8.md) |
| Hand-written single page | [Club Website](page_14.md) |

All three deploy via GitHub Pages. See [the site pattern](page_16.md) for the renderer's contract.
