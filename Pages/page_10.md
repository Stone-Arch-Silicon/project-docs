# Track: hardware and research

Two designs outside the course. Both are one-author projects, both are further along on paper than in silicon, and both are honest about it.

| Repo | Design | Stage |
| --- | --- | --- |
| [Systolic Matrix Multiplier](page_11.md) | 2x2 integer matrix multiply, SystemVerilog | Synthesis |
| [8-Bit Posit](page_12.md) | posit(8,2) arithmetic unit | Concept |

## What separates them

The matrix multiplier has **RTL and a clean Vivado synthesis run**, and is blocked on a pin-count problem. The posit project has **no RTL at all** — it has a specification, a staged build plan, and an interactive teaching tool.

```text
Mat Mul    spec → RTL → sim → synth → [blocked: 130 pins / 106 available]
Posit      spec → [next: Python golden model] → RTL → sim → OpenLane
```

## The common failure to avoid

Both repos show the same lesson from opposite sides: **a design is only as trustworthy as its checks.** The matrix multiplier simulates, but its testbench has no assertions, so "passing" means a human liked the waveform. The posit project has no code yet but already specifies an exhaustive test over all 256 codes.

Write the self-checking test first. See [project stages](page_3.md).

## If you want to contribute

- Matrix multiplier: add a self-checking testbench, then a serializing wrapper so it can actually be implemented.
- Posit: build the Python golden model. It is rung 0 of the plan and unblocks everything above it.
