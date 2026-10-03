# Systolic Matrix Multiplier

A 2x2 integer matrix multiplier (C = A x B) in SystemVerilog, written as a staggered accumulation wave rather than four independent MACs — a teaching analogue of TPU-style arrays.

**Stage:** synthesis. Behavioral simulation ran and synthesis completed cleanly; no implementation run exists.

## The design

```systemverilog
module mat_mul #(parameter N = 8)(
    input  logic clk,
    input  logic rst_n,                      // synchronous, active-low
    input  logic [N-1:0]   matA[1:0][1:0],
    input  logic [N-1:0]   matB[1:0][1:0],
    output logic [2*N-1:0] mat_out[1:0][1:0]
);
```

8-bit unsigned inputs, 16-bit outputs, four PE accumulators. Results are valid **5 cycles** after reset release.

Note what the RTL actually is: one flat `always_ff` block with a cycle counter `cyc` as sequencer, where each cycle hardcodes which PEs accumulate. The "A flows right, B flows down" picture in the README is the conceptual model, not the structure — there are no inter-PE registers.

## Synthesis results

Vivado 2025.2, part `xc7a35tcpg236-1` (Artix-7), 0 errors:

| Metric | Value |
| --- | --- |
| Slice LUTs | 658 (3.16%) |
| Slice registers | 132 (0.32%) |
| CARRY4 | 96 |
| DSP, BRAM | 0 |
| **Bonded IOB** | **130 / 106 = 122.64%** |

That last row is the blocker. The flat top level needs 130 pins and the package has 106, so the design **cannot be placed and routed on this part** as written. It needs a serializing wrapper that loads operands over several cycles.

## Layout

```text
...srcs/sources_1/new/mat_mul.sv     the entire RTL, 56 lines
...srcs/sim_1/new/tb_mat_mul.sv      the only testbench
...runs/synth_1/                     utilization report, .dcp, logs
...sim/sim_1/behav/xsim/             sim logs and waveform database
README.md                            interface table, cycle schedule, screenshots
```

The `.xpr` project file is **not committed**, so the Vivado project cannot be reopened — recreate it from the two `.sv` files.

## What is missing

- **The testbench has no assertions and no `$display`.** Four directed cases exist with expected values written only as comments; pass/fail was decided by eye. There is no headless regression.
- No constraints file, no timing analysis, no post-synthesis simulation.
- **Parameterization is broken below N = 8.** `cyc` is `[$clog2(N)-1:0]`, so for N = 4 the counter wraps before the output-latch cycle and `mat_out` is never written.
- No `valid`/`done` output; back-to-back operations require a reset pulse between them.
- The README's performance comparison table is an unmeasured claim — no baseline exists in the repo.
- Vivado binaries (`xsimk.exe`, `.wdb`, `.obj`) are committed; the repo needs a `.gitignore`.
