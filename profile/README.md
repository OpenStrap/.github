![OpenStrap](https://raw.githubusercontent.com/OpenStrap/.github/main/profile/banner.png)

# OpenStrap

Your WHOOP band doesn't stop working when the subscription does — the app just goes
dark. OpenStrap is what I built so a 4.0 band that would otherwise sit in a drawer keeps
doing something: read your own data off it over Bluetooth, keep the raw bytes, and turn
them into the numbers you actually look at.

**Everything runs on your phone.** The band talks to the app over Bluetooth, the app
decodes the bytes, computes the metrics, and stores the results locally. There's no
account, no cloud, and no server that ever sees your raw data. That isn't a privacy
setting you switch on — it's the architecture.

Is it a replacement for WHOOP? No, and I'm not going to pretend it is. They've got years
of research and a whole team; this is one person and textbook methods. But it's a real
second life for hardware you already own, and your data stays yours.

Tested on WHOOP 4.0 only. Once you start using it, don't reconnect the band to the
official WHOOP app — a firmware update could change or break the events this relies on.

### Get the app

- **iOS** — [join the TestFlight beta →](https://testflight.apple.com/join/2BVSwq65)
- **Android** — [download the APK →](https://github.com/OpenStrap/edge/releases/latest)

### The pieces

- **[edge](https://github.com/OpenStrap/edge)** — the phone app, and where everything
  actually happens: Bluetooth, local storage, the compute pipeline, every screen.
- **[protocol](https://github.com/OpenStrap/protocol)** — the decoders. Raw WHOOP 4.0
  record bytes into named fields. Pure Dart, zero dependencies, runs on-device.
- **[analytics](https://github.com/OpenStrap/analytics)** — the math. Published,
  peer-reviewed methods (Banister TRIMP, Cole-Kripke, Lomb-Scargle and friends) turn heart
  rate and motion into metrics — each carrying its own confidence and tier, and returning
  nothing rather than guessing when the data isn't there.
- **[research](https://github.com/OpenStrap/research)** — the lab notebook. The protocol
  written down, plus a one-file Python client so you can talk to a band from a terminal.
- **[backend](https://github.com/OpenStrap/backend)** — *optional, and not required.* A
  small self-hostable companion for importing an old cloud account and for opt-in
  telemetry. The app doesn't need it and doesn't use it by default.

### A few honest notes

There are bugs. Please open issues as you find them and I'll work through them. A lot of
the protocol — the events especially — is empirical guesswork, and no one person can
confirm it to 100%. The more people poke at it, the closer we get to nailing every field
down with real confidence.

The metrics are approximations built from published research, not medical-grade
measurements. Nothing here is a diagnosis.

### The people who built it

<a href="https://github.com/OpenStrap/edge/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=OpenStrap/edge" alt="Contributors" />
</a>

Mostly by wearing it on a real wrist and reporting what came out wrong — which is
genuinely the most useful thing anyone can do here, since there's one person's
physiology in the test data otherwise.

---

<div align="center">

### ☕ Like it? Help keep it going.

**No subscription, no paywall, no company behind this.**<br>
If OpenStrap gave your band a second life, a small tip genuinely helps.

**Bitcoin**

`bc1qvtcch38dcwp967ar764uu6eetw7tf907844wfq`

**EVM** — Ethereum · Base · Arbitrum · Optimism · Polygon

`0x8310C89393366b7eBCD47ABa82e1dfB5ECeFFbD9`

[**What donations actually pay for →**](https://github.com/OpenStrap/edge/blob/main/DONATE.md)

*Nothing is gated behind paying, and nothing ever will be.*

</div>

---

Not affiliated with, endorsed by, or connected to WHOOP. "WHOOP" is their trademark, used
only to say which device this talks to. MIT licensed.
