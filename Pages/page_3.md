# Project stages and the evidence they require

Every hardware project here states one stage. The rule is simple: **claim the stage your artifacts prove, and name the next missing step.**

## The ladder

| Stage | Proven by |
| --- | --- |
| Concept | A written spec and interface |
| RTL | Synthesizable source that elaborates |
| Simulation | A self-checking testbench and its pass/fail output |
| Synthesis | A gate-level netlist plus area and timing reports |
| Routed layout | A placed-and-routed database and DRC/LVS results |
| Fabrication | A tapeout record for a specific shuttle |
| Bench measurement | Lab data from physical parts |

A stage is not reached by intending to reach it. A netlist is not a layout; a layout is not a chip; an FPGA estimate is not an ASIC measurement.

## What every project records

```text
source revision (commit hash)
tool names and versions
PDK name and version
constraints actually applied
reports, logs, and waveforms
which checks passed, which are unresolved
```

## Current stages

| Project | Stage |
| --- | --- |
| [ASIC 101](page_5.md) | Course material in development |
| [ASIC Tutor](page_6.md) | In development, private |
| [ASIC Docs](page_8.md) | Scaffolded |
| [ASIC Docs Theme](page_9.md) | Usable |
| [Systolic Matrix Multiplier](page_11.md) | Synthesis |
| [8-Bit Posit](page_12.md) | Concept |
| [Club Website](page_14.md) | Live |
| [Org Profile](page_15.md) | Live |

Stages move when evidence lands in the repo, not when work feels done. Verify a stage against the project's own page before citing it.
