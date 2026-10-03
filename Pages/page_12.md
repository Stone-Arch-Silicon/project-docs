# 8-Bit Posit

A UMN UROP project designing an 8-bit **posit** arithmetic unit. This repo holds the specification and the build plan for the **codec** — the decoder and encoder — plus an interactive teaching tool.

**Stage:** concept. No RTL, no testbench, no model. Two files: a 50-byte README and one self-contained HTML manual.

## The format: posit(8, es = 2)

```text
[ sign : 1 ][ regime : 1-7, run-length coded ][ exp : 0-2 ][ fraction : 0-3 ]
```

Only the sign field has fixed width. Value is `(-1)^s x useed^k x 2^e x 1.f` with `useed = 2^(2^es) = 16`.

| Quantity | Range |
| --- | --- |
| Regime k | -6 to 6 |
| Exponent e | 0 to 3 |
| Scale = 4k + e | -24 to +24 (signed 6 bits) |
| Significand | 8 to 15, hidden bit included |
| maxpos, minpos | 2^24, 2^-24 |
| Quire width | 128 bits (32 guard / 48 int / 48 frac) |

`0x00` is zero, `0x80` is NaR — one value replacing both NaN and the infinities. That leaves 254 nonzero reals. Negative inputs are two's-complemented before decoding.

## The architecture principle

Every posit operation is the same three stages: **decode both operands, do plain integer arithmetic, encode once at the end.** The middle stage never sees a posit.

The key interface decision is two structs, not one — a 4x4 significand multiply is 8 bits wide and product scale reaches ±48, so the decoder's output type cannot serve the encoder's input. The encoder owns all normalization and rounding, which is why it is expected to dominate codec area.

## The interactive manual

`posit8_codec_manual.html` — one file, no framework, no build. Its live byte explorer reimplements the decoder in ~130 lines of JS: click any bit, watch the **field boundaries move** as the regime run-length changes, and read out sign, k, e, scale, significand, and value. Increment and decrement buttons demonstrate that stepping the integer always steps to the next posit.

Use it to check a Python model before trusting that model to check RTL.

## The build ladder

```text
0  Python golden model over all 256 codes        ← next step
1  regime_count module, all 128 payloads
2  full decoder, all 256 codes bit-for-bit
3  truncating encoder, round-trip identity
4  round-nearest-even + clamping
5  codec alone through OpenLane on SKY130
```

Rung 5 is the funded deliverable — area, critical path, and Fmax for the codec standalone — and it does not depend on anyone else's block.

## Three things to settle before writing RTL

1. **SoftPosit does not implement posit8 with es = 2.** Its `posit8_t` is es = 0. Verify against it and every test fails for the right reason. Use Stillwater Universal or a hand-written model.
2. **Version the two-struct interface now**, in the repo, before anyone starts their block.
3. **Tiny Tapeout pin budget constrains the top level.** Two 8-bit operands plus an opcode do not fit in 8 input pins; use the bidirectional pins or load over two cycles. Separately, a 128-bit quire will not fit in one tile — price out a multi-tile submission early.

## What is missing

Everything below the specification. The README carries no information, GitHub Pages is not enabled, and there is no license file.
