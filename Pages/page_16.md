# The shared toolchain

Every project draws from the same small set of tools. Learn these once and they carry across the whole org.

## By job

| Job | Tool |
| --- | --- |
| Design | Verilog / SystemVerilog |
| Simulation | ModelSim, Vivado simulator |
| FPGA implementation | Vivado, AMD/Xilinx parts |
| Open-source ASIC flow | LibreLane |
| Process technology | SKY130 |
| Professional EDA | Cadence, via club and university resources |
| Documentation | mdBook, plus the markdown site pattern |

The ASIC learning track is deliberately open-source: LibreLane and SKY130 install on a student laptop and need no license server. Cadence is for work that genuinely requires it.

## Reference designs we read

- [PicoRV32](https://github.com/YosysHQ/picorv32) — a small, readable RISC-V core
- [CVA6](https://github.com/openhwgroup/cva6) — an application-class core, for seeing how a real project is organized

## What to record, always

```text
tool name and exact version
PDK name and version
the constraint file actually used
the commit hash of the RTL
```

Without those four, a report cannot be reproduced or compared, which makes it evidence of nothing. See [project stages](page_3.md).

## Beyond the club

Stone Arch Silicon participates in the [ASIC Network](https://github.com/ASIC-Network), which hosts [analog](https://github.com/ASIC-Network/analog-tutorials) and [digital](https://github.com/ASIC-Network/digital-tutorials) tutorial tracks shared across member clubs.

## The markdown site pattern

[ASIC 101](page_5.md) and this site share one renderer: `index.html` + `style.css` + `app.js`, no build step and no dependencies. Porting it means copying `app.js` and `style.css` **verbatim**, editing `CONFIG` at the top of `app.js`, and editing about ten branding strings in `index.html`.

The `CONFIG` knobs:

| Field | Controls |
| --- | --- |
| `title` | Tab title and the subtitle under the wordmark |
| `repo` | GitHub nav link and the per-page edit link |
| `mainSite` | Where the brand mark and "Club" link go |
| `org`, `orgMark` | Title suffix and the wordmark text |
| `branch` | The `/edit/<branch>/` segment of the edit link |
| `pagesDir` | Folder holding the markdown; also the base for relative image paths |
| `maxPages` | Upper bound of the discovery scan, not a page count |
| `unitWord` | The "Page 07 / 17" label; pluralized naively by appending `s` |

The discovery contract, which is strict:

```text
<pagesDir>/page_<N>.md    N starts at 1, no zero padding in the filename
exactly one "# " heading   it becomes the sidebar label
contiguous numbering       the first missing number ENDS discovery
served over HTTP           discovery uses fetch(); file:// shows an error
raw HTML                   escaped; markdown only
```

A gap in the numbering silently hides every page after it. That is the one failure mode worth remembering.

Table of contents is built from `h2` and `h3` only. A markdown link matching `page_N.md` is rewritten to the in-page route `#page_N`; anything else resolves against `pagesDir`.
