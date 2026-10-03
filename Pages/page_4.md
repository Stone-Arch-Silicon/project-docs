# Track: curriculum

Two repos, one job: get a student from "I know Verilog syntax" to "I have hardened a block and can defend the reports."

| Repo | Role | Stage |
| --- | --- | --- |
| [ASIC 101](page_5.md) | The course. Reading, one long project, real EDA tools. | In development |
| [ASIC Tutor](page_6.md) | The drill ground. Small graded exercises, offline. | Early, private |

## The split

ASIC 101 is **one design carried the whole way** — an 8-bit ALU, 25 lessons, RTL to GDSII. It is slow by design, and the tools are the real ones.

ASIC Tutor is **many small problems, each graded in seconds** by Verilator. No PDK, no flow, no network. It stops at simulation.

```text
ASIC Tutor   → reps, fast feedback, one concept per problem
ASIC 101     → one project, full depth, real reports
```

## Not yet wired

The intended link is bidirectional — a lesson saying "drill this in Tutor," a Tutor problem saying "now take it through the flow." Today ASIC 101 does not reference ASIC Tutor at all. That link is unbuilt.

Tutor is also still a private repository, so for now the only track a newcomer can actually start is ASIC 101.

## Suggested order

1. ASIC 101 lessons 1–9 — RTL, verification, FPGA.
2. ASIC 101 lessons 10–25 — the ASIC flow and the capstone comparison.
3. Tutor exercises alongside, once you have access.
