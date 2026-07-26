# Contributing to OpenStrap

This is the org-wide default. The three main repos — [protocol][p],
[analytics][a], [edge][e] — each have their own `CONTRIBUTING.md` with
repo-specific detail, and those override this one. Read theirs if you're working
there.

## First: which repo?

This is the thing that most often sends a PR to the wrong place, so it's worth
30 seconds up front.

| Your change | Repo |
|---|---|
| A record type, opcode, event — anything about the bytes on the wire | [**protocol**][p] |
| A metric, or how an existing number is computed | [**analytics**][a] |
| Bluetooth, storage, background sync, UI — anything app-shaped | [**edge**][e] |
| The optional companion worker (legacy import, update pointer, opt-in telemetry) | [**backend**][b] |
| Protocol notes, or the standalone Python client | [**research**][r] |

The separation is strict and it's load-bearing: protocol has zero dependencies,
analytics has zero runtime dependencies and no I/O, and edge is the only thing
that touches a device. If you're unsure, open an issue and ask — that's cheaper
than moving code between repos afterwards.

## The rules that apply everywhere

**Never fabricate a number.** If an input isn't there, the result is `null` — not
a default, not a last-known-good, not an interpolation that will look fine on a
chart. Every metric carries a confidence and a tier (`AUTH` / `HIGH` /
`ESTIMATE` / `RELATIVE`). A metric that quietly invents a value when the data is
missing is worse than no metric at all, because you can't tell the difference
from the outside.

**Cite the method.** Anything computing a physiological quantity implements a
published, peer-reviewed algorithm, cited in a comment next to the code. If
nothing in the literature fits, that's allowed — mark it `ESTIMATE`, give it low
confidence, and say so. What isn't allowed is inventing constants and presenting
them as science, or fitting to WHOOP's outputs to match their scores.

**Some limits are real, not bugs.** HRV here is PRV from 1 Hz beat timing. Deep
sleep is a low-confidence HR-flatness overlay. SpO₂ and skin temperature are
relative ADC values with no calibration to absolute units. These are properties
of what the band actually hands over. Please don't "fix" them by making output
look more confident than the input supports.

**Don't overclaim on privacy either.** The same honesty standard applies to what
we say about data. Everything health-related is computed and stored on-device;
where that's qualified — anonymous diagnostics in GitHub builds, opt-in
contribution, BYOK AI prompts that contain your metrics — say so plainly rather
than rounding it to "no cloud".

## Provenance

Facts about a wire protocol, worked out by observing a device you own, are fine
and are what this project is built on.

Vendor source code, firmware, decompiled binaries, and material from other
reverse-engineering projects whose licences don't permit reuse are **not** — in
code, comments, commit messages, or PR descriptions. Several projects in this
space are unlicensed (which means all rights reserved, not public domain) or
non-commercial-only. OpenStrap is MIT and stays cleanly MIT.

## Pull requests

- Branch off `main`. One logical change per PR.
- Explain *why*, not just what. Link the issue if there is one.
- Say how you verified it. For protocol work, "decoded N real records off my own
  band and the values were plausible" is a genuinely good answer.
- If it changes any number a user sees, say so explicitly — that's the single
  most important line in the PR, because stored results are versioned and a
  change means `kAlgoVersion` has to be bumped in edge.
- CI runs analyze + the full test suite on every PR. Please get it green.
- No `Co-Authored-By` trailers.

## Reporting things

- **A bug, or a metric that looks wrong** — [edge issues][ei]. There's a form for
  each; the metric one exists because "it doesn't match the WHOOP app" isn't by
  itself a bug.
- **A protocol finding** — [protocol issues][pi]. Include the bytes and how you
  convinced yourself.
- **A security problem** — privately, please. See `SECURITY.md`.

[p]: https://github.com/OpenStrap/protocol
[a]: https://github.com/OpenStrap/analytics
[e]: https://github.com/OpenStrap/edge
[b]: https://github.com/OpenStrap/backend
[r]: https://github.com/OpenStrap/research
[ei]: https://github.com/OpenStrap/edge/issues/new/choose
[pi]: https://github.com/OpenStrap/protocol/issues/new
