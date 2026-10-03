# ASIC 101

A 25-lesson course that carries **one 8-bit ALU** from Verilog to a GDSII layout. Public repo, static site, no build step.

**Stage:** course material in development. Finishing the lessons produces a design and an evidence package — not a fabricated or measured chip.

## The course map

| Stage | Lessons | You produce |
| --- | --- | --- |
| Orientation | 1–2 | Workspace and an understood spec |
| RTL | 3, then **one of** 4/5/6 | ALU with a custom adder |
| Verification | 7 | Self-checking testbench and results |
| FPGA | 8–9 | Timing, utilization, power, interpretation |
| ASIC setup | 10–13 | Environment, constraints, baseline run |
| Physical design | 14–19 | Stage views and reports |
| Signoff | 20–23 | Timing, connectivity, physical-rule evidence |
| Capstone | 24–25 | Architecture comparison and handoff |

Lessons 4, 5, and 6 are an **exclusive choice** — ripple carry, carry lookahead, or carry select. All three paths rejoin at lesson 7. Lesson 7 exercises all 524,288 input combinations of the combinational ALU.

## The reference design

`files/alu/` is shared by all three adder tracks:

```text
rtl/      adder8_{rca,cla,csel}.v, alu_core.v, alu_top.v
tb/       directed, exhaustive, and clocked-scoreboard testbenches
cocotb/   Python reference model, constrained-random, coverage
formal/   SymbiYosys properties + a deliberately buggy ALU to catch
tt/       Tiny Tapeout wrapper (tt_um_sasi_alu)
pd/       LibreLane config: alu_top, 10.0 ns clock, 110x110 um die
```

One Makefile drives it, parameterized by adder:

```sh
cd files/alu
make check ADDER=rca     # lint, sim, formal, synth
```

## Stack

Verilog-2001/2012, Icarus + Verilator + cocotb, SymbiYosys, Yosys, LibreLane 3.0.14, SKY130A with `sky130_fd_sc_hd`, Vivado for the FPGA track. CI runs the full matrix over `rca`/`cla`/`csel` on every push.

## Start here

Read `Pages/page_1.md`. To preview the site locally:

```sh
python3 -m http.server 8000
```

## What is missing

- Validate the course from a clean environment.
- Record a reference ALU run; publish comparable RCA/CLA/carry-select results under identical constraints.
- Verify internal links and downloads.
- Add lesson ownership and review dates — the README requires an **Authors and reviewers** section per lesson and **no lesson has one**.
- `files/tutorial_files.md` is still a placeholder.
- The reference-run workflow uses `continue-on-error`, so runs publish even when the flow fails. Check `flow-outcome.txt` before trusting a reference run.

[Repo](https://github.com/Stone-Arch-Silicon/ASIC_101) · [Site](https://stone-arch-silicon.github.io/ASIC_101/)
